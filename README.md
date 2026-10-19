# H200 Usage Explorer

An interactive, single-page view of GPU usage on a shared **NVIDIA H200 NVL** (143,771 MiB / 140.4 GiB), broken out **by user and by hour** for each day the GPU was held. Pick a day to see memory held, utilization and free capacity across the whole day, open any hour for the per-user split, and read the job kill/cancel events annotated on the timeline.

**[Open `index.html`](index.html)** in a browser, or enable GitHub Pages for this repo to view it online.

## What it shows

- **Day selector** — one tab per day with GPU activity.
- **Summary tiles** — average GPU util, peak memory used, minimum free, peak concurrent users, and your own peak memory / average util.
- **Whole-day charts** — GPU utilization (whole-GPU area plus per-user lines) and a stacked memory chart (per-user GiB held → unattributed overhead → free, up to the 140.4 GiB ceiling). Hover for exact values.
- **Job events** — dashed markers on the charts flag crashes (red), jobs killed by root/scheduler (amber) and self-cancels (grey).
- **Hourly table** — per hour: GPU util (mean/peak), memory used (mean/peak), free (mean/min), active users, and your footprint; expand any hour for the per-user breakdown.

## Data

`h200_data.json` holds hourly aggregates and per-minute series. It is built from two monitors over **2026-10-10 → 2026-10-19 (IST, UTC+5:30)**:

- **Oct 10–11** — a ~10 s H200 sampler log.
- **Oct 15–19** — a gpu-watch daemon log (~5 min Oct 15–17, ~15 min Oct 18–19).

Each day carries its own cadence and source, shown in the UI; the coarser days have fewer points per hour.

Memory is in GiB (1 GiB = 1024 MiB). "Unattributed" is whole-GPU memory not charged to a named process (CUDA context / driver overhead). Per-process utilization can exceed the single whole-GPU figure when jobs overlap.

## Privacy

All users other than the repository owner are **anonymized** to `user-01 … user-12` (ranked by peak memory footprint). No real usernames of other people appear in this repository.
