# DREAM: Disaster Response Queueing Model

Python tool built during an internship to help plan staffing for mass casualty incident (MCI) response. It models how casualties move through stages in disaster response: Hot Zone, Casualty Collection Point, Staging Area, and Advanced Medical Post, and estimates whether the current number of teams can keep up with incoming casualties.

User Manual: https://docs.google.com/document/d/12MXNLDTKlQ0HM1NfmpoTbaPHug6XjJ3uvQhEK5yXPkE/preview?rm=minimal

## What it does

**Data collection.** A menu-driven interface logs casualty timing data (dispatch, arrival, treatment, transport timestamps), saved locally as JSON. Supports add, view, edit, and delete, plus configurable team counts and capacity per stage.

**Queueing model.** Uses the logged data to estimate arrival and service rates per stage, then models each stage as a multi-server queue (M/M/c, or a finite-capacity variant if a max casualty capacity is set). For each stage it computes:
- Expected number of casualties in the system and in queue
- Expected time in system and time waiting
- Team utilization
- Probability distribution of casualty counts, plotted per stage

If a stage can't keep up with incoming casualties, the tool flags it and can suggest a stable team/capacity setup.

**Recommendations.** Generates plain-language notes on utilization (under-used, optimal, at risk of overload) and on the probability distribution (most likely casualty count, overload risk), plus a combined summary across all stages showing the system bottleneck.

## Stack
Python, pandas, matplotlib. Built and run in Google Colab.

## Mobile app
The same model is also built as a Flutter app for Android, so it can be used directly in the field instead of through the notebook. It has three tabs:

- **Input** — enter casualty timestamps (SAR dispatched, CCP arrival, first aid returned, SA arrival, transport returned), with quick +1/+5 minute adjustment buttons and auto-adjust for adjacent times. Also where team counts and capacity are set for each stage.
- **Data** — list of logged entries, editable and deletable, with the running average rates shown at the bottom.
- **Metrics** — the queueing results for both stages: recommendations, stability notes, and a probability distribution chart (bar chart, via fl_chart).

Same stages (Casualty Collection Point, Staging Area) and same queueing formulas (M/M/c, with finite-capacity variants) as the notebook, reimplemented in Dart. Data is stored locally on the device (shared_preferences), and the app runs fully offline.

