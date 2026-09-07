# Robot Navigation Testing Lab

A browser-based lab for **SJSU CMPE 187 (Software Quality Engineering)**.
Students do not write code and install nothing. They pick a robot, set a handful
of documented inputs, run a real simulation, and read a Pass/Fail verdict with
the measurements behind it.

It runs in **MATLAB Online**, which SJSU licenses campus-wide, so any laptop with
a browser will do — no download, no GPU, no version pinning, and nothing for
macOS to block.

## Running it

Sign in to MATLAB Online through the
[SJSU MathWorks portal](https://www.mathworks.com/academia/tah-portal/san-jose-state-university-31511582.html),
then paste this into the Command Window:

```matlab
websave('getlab.m','https://raw.githubusercontent.com/ganeshsjsu/robot-testing-lab/main/matlab/getlab.m'); getlab
```

Then:

```matlab
labselftest     % three cases and every robot, to check it works
testlab         % opens the lab
```

## What is under test

A robot must drive from a start pose to a goal inside a square arena without
hitting anything. It carries a three-beam range sensor at 0° and ±25°, position
and heading sensors, and **no map** — it steers at the goal and turns away from
what the beams see. The failures students find are the real limits of that
design, not planted bugs.

| | |
|---|---|
| Robots | e-puck, TurtleBot3 Burger, TurtleBot3 Waffle, Pioneer 3-DX, Clearpath Jackal, Clearpath Husky, and small and large car-like models |
| Scenarios | open field, single obstacle, corridor, dogleg, clutter |
| Arena | square, 1–6 m, every scenario scales with it |
| Requirements | reach the goal in time, no collision, 0.03 m clearance, stay inside, reject undocumented input |

The robots carry their real published dimensions, from 7 cm to 80 cm across, and
the sensor, controller and requirements are identical for all of them — so any
difference in verdict is caused by the machine and nothing else.

## Layout

```
matlab/LAB_HANDOUT.md     hand this to students
matlab/ANSWER_KEY.md      instructor only: every boundary, measured
matlab/labspec.m          single source of truth: robots, scenarios, ranges, requirements
matlab/labvalidate.m      REQ-5 input validation
matlab/lablayout.m        scenario geometry
matlab/labhalf.m          where the wall is, for a given arena size
matlab/labrun.m           simulate, measure ground truth, judge
matlab/testlab.m          the student UI
matlab/labselftest.m      pass, fail and rejected cases plus every robot
matlab/getlab.m           pull the latest files from here
```

`labspec.m` is the single source of truth. The form students see is generated
from it, so the ranges displayed and the ranges enforced cannot disagree.

## Why not Webots

The lab was first built on Webots, which is the better teaching simulator. It
could not be shipped to a class: its macOS installer is not notarised, so macOS
blocks it with a malware warning, and Homebrew disabled its `webots` cask on
2026-09-01 for exactly that reason. Asking a software-quality class to click past
a malware alert was not defensible. That implementation is in this
repository's history up to commit `767eb58` if it is ever needed again.

Gazebo and NVIDIA Isaac Sim were also considered and rejected — Gazebo requires
students to write ROS code, and Isaac Sim needs an RTX 4080 and 32 GB of RAM and
does not support macOS at all.
