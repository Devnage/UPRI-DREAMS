# DREAM: Disaster Response Queueing Model

Python tool built during an internship to help plan staffing for mass casualty incident (MCI) response. It models how casualties move through three stages: Search & Rescue, First Aid (Casualty Collection Point), and Transport (Staging Area), and estimates whether the current number of teams can keep up with incoming casualties.

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

## Notes
Built solo (programming). The queueing formulas and MCI process model were worked out and checked with a small team during the internship. This notebook is the modeling core of the project; the model was later carried over into a Flutter mobile app prototype.
