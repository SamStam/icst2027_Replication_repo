# Replication package

Logged flight traces and the analysis that produces the numbers reported in
the paper.

The experiments themselves need a Crazyflie 2.1 and a two-base-station
Lighthouse setup. **The analysis does not.** Every table in the paper is
recomputed here from the traces in `data/`, with no hardware and no network
access.

## Running it

```
pip install numpy pandas jupyter
jupyter notebook reproduce.ipynb     
```


```

`reproduce.ipynb` is shipped with its outputs so the results can be read without running anything.

## What produces what

| Notebook section | Paper |
|---|---|
| Admission | Section V-D, and the flight counts in Section V-B |
| Table I | conformance verdict per mission |
| Table II | robustness of the square band |
| Table III | fault-injection campaign |
| Admission in practice | Section VI-E |

## Data

```
data/physical/square/              square mission, measurement batch
data/physical/excitation/          excitation mission, all flights flown
data/physical/square_relocalised/  square traces rejected on plausibility
data/physical/handover/            vehicle-replacement runs + faults
data/twin/                         traces produced by the digital twin
```

One CSV per flight, 50 Hz. Columns: `t_mission` (s, from takeoff), `x y z`
(m, Lighthouse frame), `yaw`, `vx vy vz`, `vbat` (V), `sp_x sp_y sp_z sp_yaw`
(commanded setpoint), `phase`, `note`. `run_id` is the trace identifier used
in the printed output.

Rejected flights are included on purpose: the admission conditions are a
result of the paper, and they cannot be checked against admitted traces
alone.

The two missions are analysed over the windows given in Section V-B,
[5, 20] s for the square and [8, 38.5] s for the excitation. 

## A note on the handover band
The handover errors were collected online by the supervision service at the decision points. They are reported as runtime measurements and are not recomputed from the released flight traces



