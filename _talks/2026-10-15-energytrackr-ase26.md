---
title: "EnergyTrackr: A Modular Energy Regressions Detection Tool"
collection: talks
type: "Presentation"
permalink: /talks/2026-10-15-energytrackr-ase26
venue: "International Conference on Automated Software Engineering"
date: 2026-10-15
location: "Munich, Germany"
---

[Slides](https://jeromemaquoi.github.io/files/bechet-2026-slides.pdf)

## Abstract

Energy efficiency is increasingly recognized as an important dimension of software quality. As systems evolve rapidly, tracking how energy consumption changes across versions can provide valuable insights for developers and researchers. Although detecting energy regressions (i.e., unintended increases in energy consumption) remains challenging due to measurement variability and complex execution environments, recent advances now make systematic analysis practical. Still, dedicated support for monitoring energy behavior over a project’s history is missing. This paper presents EnergyTrackr, a modular, open-source tool for automatically detecting, classifying, and visualizing energy regressions across a commit history. EnergyTrackr traverses a specified set of commits, builds each revision, and measures application-level energy consumption by executing the test suite using the RAPL-based Linux perf utility. It applies established best practices for measurements such as warmup, randomized execution, repetition, and thermal control. The resulting data are analyzed through a statistical pipeline that filters outliers and classifies energy changes using multiple criteria (e.g., significance, practical impact, ...). EnergyTrackr generates interactive reports that provide a comprehensive view of energy evolution and is designed for easy integration into existing Linux workflows. A preliminary evaluation on large Java projects shows that EnergyTrackr can produce stable measurements at scale and effectively identify energy regressions.
Source: [https://github.com/snail-unamur/energytrackr](https://github.com/snail-unamur/energytrackr)
Screencast: [https://doi.org/10.5281/zenodo.21507425](https://doi.org/10.5281/zenodo.21507425)
