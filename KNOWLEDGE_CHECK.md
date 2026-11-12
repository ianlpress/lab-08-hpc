# Lab 08: Knowledge check

## 1. Slurm: what jobs have I submitted?

sacct -u $USER -S 2026-11-04 --format=JobID,JobName,NodeList,Partition,Account,User,State,Start,Elapsed > results/job-history.txt

## 2. Slurm: did every array task run at the same time?

No. Tasks 1–2 started at 18:50:36 and tasks 3–7 at 18:51:26, because Slurm schedules each array task separately and starts it only when a GPU slice on the shared gpu-mig node is free (and within my per-user limit). The elapsed times were similar but not identical (14–17 s), since books differ in length and each task loads the model separately.

## 3. Slurm: did my job use what it asked for?

One task used 3.09 GB of the 16 GB I requested (19%) and about 15 seconds of the 5-minute limit. For 1,000 books I would lower the request to about --mem=6G and --time=00:02:00, which still leaves a safety margin. Smaller requests are easier for the scheduler to fit, so tasks can start sooner, and they don’t block resources other users could use.


