# Camp Carysbrook · Staff Scheduler (hours-off-scheduler_V2)

A Streamlit app for generating day-off schedules for camp staff and counselors.

This repository contains a single-file Streamlit application (streamlit_app.py) that
creates balanced day-off assignments while respecting cabin, leadership, and activity
constraints. It is intended for use at Camp Carysbrook but can be adapted for other
small-team scheduling needs.

## What's in this repository

- streamlit_app.py — The main Streamlit application (single-file). Features:
  - Upload CSV or XLSX of counselor data (required columns listed below).
  - Integer programming solver (PuLP) to assign days off while enforcing:
    - Per-day maximum counselors off
    - At most one counselor from the same cabin off on the same day
    - Activity and leadership capacity limits to avoid too many of the same role/activity off on one day
    - Soft objective to minimise peak number of seniors off at the same time
  - Preview table, per-day summary chart, and downloads (CSV and colour-coded Excel).
  - Customised Camp Carysbrook styling and downloadable CSV template.

- requirements.txt — Minimal dependencies used by the app (Streamlit, pandas, PuLP, ...).
- LICENSE — Project license (Apache-2.0).
- .github/, .devcontainer/ — Configuration and automation files.

## Required input format

Upload a CSV or XLSX file containing the following columns (exact names expected):

```
Name, Cabin, Leadership, Activity1, Activity2, Age
```

Leave cells blank where not applicable. A downloadable template is available from the app sidebar.

## How to run locally

1. Install requirements:

   ```bash
   pip install -r requirements.txt
   ```

2. Run the Streamlit app:

   ```bash
   streamlit run streamlit_app.py
   ```

3. In the sidebar you can:
   - Choose the schedule window length (3–7 days), number of days off per counselor, and maximum counselors off per day.
   - Download a template CSV showing the required columns and example rows.

4. Upload your counselor spreadsheet, preview the data, and click "Generate Schedule". You can then download the resulting schedule as CSV or Excel.

## Notes and dependencies

- The app uses PuLP as the solver backend. Installers may need to also install a solver (PuLP includes CBC by default).
- Excel export uses openpyxl. If Excel download raises an ImportError, install openpyxl:

  ```bash
  pip install openpyxl
  ```

- The app includes custom CSS for Camp Carysbrook branding (fonts, colours, header/footer).

## License

This repository is licensed under the Apache License 2.0. See LICENSE for details.
