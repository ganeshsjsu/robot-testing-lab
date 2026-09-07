# Demo run order

Five minutes. Sign in to MATLAB Online, paste the bootstrap line, then `testlab`.

| # | Set | Point to make |
|---|---|---|
| 1 | defaults, press **Run test** | Set inputs, watch it drive, get PASS with the measurements behind it. No code. |
| 2 | Wheel speed `99` | REJECTED before anything runs, naming the parameter and the legal range. |
| 3 | Wheel speed `2.0` | FAIL — times out. Same robot, same arena, legal input, different verdict. |
| 4 | Robot → `PIONEER_3DX` | Same test, bigger robot, different result. Eight robots are available. |
| 5 | Robot → `CLEARPATH_HUSKY` | REJECTED: an 0.80 m robot does not fit a 2 m arena. Set Arena size to `5`, run again. |

Close with the test log and **Download log as CSV**.

## What to ask Radhika

The tool does more than any one assignment needs. These are hers to decide:

- Which robots and scenarios to expose, or all of them
- How many test cases students run, and whether they design them or are given them
- What students submit — video, CSV log, written report, or some combination
- Whether input validation (REQ-5) is part of the assignment or just a safety net
- Whether the five requirements stand as written

Once she answers, the assignment is an afternoon.
