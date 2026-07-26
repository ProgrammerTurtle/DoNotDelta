# Colinear Delta Kinematics

This document describes Kalico's `colinear_delta` kinematics: what the machine
is, how to configure it, how it homes, and how to calibrate it. For the
firmware-implementer's view (the math, the source layout, and how to extend
this class of kinematic), see
[Colinear_Delta_Agent_Guide.md](developers/Colinear_Delta_Agent_Guide.md).

## Overview

A **colinear delta** is two independent linear-delta mechanisms that share the
same three physical vertical rails - hence "colinear":

- A **toolhead delta** (`stepper_a`, `stepper_b`, `stepper_c`) moves the nozzle.
- A **bed delta** (`stepper_d`, `stepper_e`, `stepper_f`) moves the build plate.

Each of the three rails carries **two carriages** - an upper one belonging to
the toolhead delta and a lower one belonging to the bed delta - so the machine
has **six motors** and **six endstops**.

Because both the nozzle and the part move, what matters for printing is their
**relative** position. Kalico therefore treats the commanded coordinate
`P = (X, Y, Z)` as *the position of the nozzle relative to the part* and shares
each move between the two mechanisms:

- The toolhead performs a `motion_split` fraction of the move (default `0.5`).
- The bed performs the remainder, `1 - motion_split`.

Splitting the motion lets each mechanism travel less and accelerate less for a
given relative move, which is the usual motivation for the design (higher
effective dynamics and/or a taller build volume).

The bed delta is mounted rotated relative to the toolhead delta. This rotation
about Z is configured with `secondary_rotation` and defaults to **180 degrees**,
which matches the common colinear delta layout where the build-plate delta sits
opposite the toolhead delta. The relative geometry the firmware enforces is:

```
(toolhead effector) - (bed effector) = Rz(secondary_rotation) * P
```

## Hardware requirements

The kinematics assume, and Kalico does not currently support otherwise:

- All six carriages ride **vertical rails** (parallel to Z).
- Each effector hangs **between** its two carriages via diagonal arms, so both
  deltas use the standard `+sqrt` delta solution (toolhead carriages above the
  nozzle, bed carriages below the plate for a 180-degree machine).
- Each mechanism homes to the **top of its own carriage travel** and the two
  mechanisms home at opposite ends of the shared rails. See
  [Homing](#homing).
- The machine is centered at home (all three carriages of a mechanism at equal
  height place that effector on the Z axis).

Tilted rails, or a mechanism whose carriages sit on the far side of its
effector (needing a `-sqrt` solution), are out of scope and would require new
firmware.

## Configuration

Set `kinematics: colinear_delta` in `[printer]` and provide six stepper
sections. See the
[colinear delta section of the Config Reference](Config_Reference.md#colinear-delta-kinematics)
for the full parameter list. A minimal skeleton:

```
[printer]
kinematics: colinear_delta
max_velocity: 300
max_accel: 3000
max_z_velocity: 150
delta_radius: 100.0
print_radius: 90.0
motion_split: 0.5
secondary_rotation: 180

[stepper_a]
step_pin: ...
dir_pin: ...
enable_pin: ...
rotation_distance: 40
microsteps: 16
endstop_pin: ...
homing_speed: 50
position_endstop: 200.0
arm_length: 250.0

[stepper_b]
# step/dir/enable/endstop pins ...
[stepper_c]
# step/dir/enable/endstop pins ...

[stepper_d]
# step/dir/enable/endstop pins ...
position_endstop: 200.0
arm_length: 250.0

[stepper_e]
# step/dir/enable/endstop pins ...
[stepper_f]
# step/dir/enable/endstop pins ...
```

Notes:

- `delta_radius` and the tower `angle` values are shared: `stepper_d` rides the
  same rail as `stepper_a`, so its angle defaults to `stepper_a`'s (and likewise
  e&harr;b, f&harr;c). You normally do not set `angle` on the bed steppers.
- `arm_length` for each bed stepper defaults to the matching toolhead stepper's
  arm length; set it explicitly only if the bed arms differ.
- `position_endstop` must be provided for `stepper_a` (toolhead) and `stepper_d`
  (bed); the other steppers in each mechanism default to those values.
- `print_radius` must be reachable by **both** mechanisms. Kalico rejects a
  configuration whose `print_radius` exceeds the radius either mechanism can
  reach for the chosen `motion_split` and arm lengths, and tells you the
  maximum. Because each mechanism only travels a fraction of the move, the
  reachable relative radius can exceed a single delta's radius.

## Homing

`G28` homes all three cartesian axes at once. Internally the two mechanisms are
homed **sequentially** because, for a relative-Z move, the toolhead carriages
and the bed carriages travel in **opposite** directions - a single coordinated
move cannot drive both sets onto endstops that sit at opposite ends of the
rails. Kalico homes the **bed** mechanism first and the **toolhead** mechanism
second, leaving the nozzle parked at its maximum distance from the part (the top
of the build volume), analogous to a normal delta homing to the top.

Endstop placement must match this: the toolhead endstops trigger at the top of
the toolhead carriages' travel and the bed endstops at the top of the bed
carriages' travel (which is the opposite end of the shared rail). Homing drives
each mechanism to the top of its own travel.

Because the mechanisms are coupled through the shared cartesian coordinate,
homing one mechanism moves the other. Ensure both mechanisms have clearance
through the full homing sweep before running `G28` on new hardware.

## Calibration

- **Arm length / delta radius / endstops.** `DELTA_CALIBRATE` calibrates the
  **toolhead** mechanism exactly as for a
  [linear delta](Delta_Calibrate.md); it adjusts `delta_radius`, the toolhead
  tower `angle`s, `arm_length`s, and `position_endstop`s. The bed mechanism is
  assumed to be geometrically symmetric to the toolhead mechanism and is not
  probed. If your bed arms or radius differ, set those bed parameters by hand.
- **Motion split.** `motion_split` is a mechanical property of how the machine
  is driven, not something `DELTA_CALIBRATE` measures. Leave it at `0.5` unless
  you are deliberately biasing motion toward one mechanism.
- **Secondary rotation.** `secondary_rotation` describes how the bed delta is
  mounted. For most machines this is exactly `180`. If prints come out mirrored
  or rotated, re-check this value (and your stepper `dir_pin` polarities) before
  changing anything else.

## Limitations and notes

- Only vertical-rail, carriage-outboard geometries are supported (see
  [Hardware requirements](#hardware-requirements)).
- `DELTA_CALIBRATE` covers the toolhead mechanism only; bed geometry is assumed
  symmetric.
- Homing choreography (order, direction, and clearances) depends on how your
  endstops are placed. Validate homing carefully on new hardware, with the
  motors free to move, before trusting `G28`.
