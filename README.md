# CMU 18-744 Autonomous Vehicle Project: Hybrid ViPlanner + D* Lite Navigation

## Overview

CMU 18-744 autonomous vehicle project: hybrid ViPlanner + D* Lite navigation in Isaac Sim.
This repository is a portfolio page for our CMU 18-744 Autonomous Vehicle project. The project extended the ViPlanner framework (forked from leggedrobotics/viplanner and modified orignally from  JiaoZA01/viplanner) with a hybrid neuro-symbolic navigation pipeline using D* Lite fallback planning, trajectory checking, occupancy-grid validation, and simulation testing in NVIDIA Isaac Sim. The original development fork was maintained at JiaoZA01/viplanner; this portfolio repo summarizes the project, results, and my contributions.

## Project Context
CMU 18-744 course project. Team project.

This was a team project for CMU 18-744 Autonomous Vehicles. The project was built on top of the open-source ViPlanner framework and modified through a team development fork maintained at `JiaoZA01/viplanner`.
The team added a hybrid navigation pipeline on top of ViPlanner. The main additions included a D* Lite fallback planner, occupancy-grid construction from depth observations, trajectory safety checking, obstacle inflation for clearance, persistent world-frame obstacle memory, planner-switching logic, and simulation testing in NVIDIA Isaac Sim using a Limo mobile robot platform.)

The goal was not to replace ViPlanner completely. Instead, ViPlanner remained the nominal learned planner, while D* Lite acted as a deterministic safety and fallback layer when the proposed neural trajectory was unsafe, blocked, or likely to collide.



## System Design
Explain ViPlanner + D* Lite + checker + occupancy grid + fallback.
The system uses a dual-path navigation design. ViPlanner generates a learned local trajectory from visual-semantic observations, while the D* Lite module builds a conservative graph-search path using an occupancy grid generated from depth data. A checker module evaluates whether the ViPlanner trajectory is safe before execution. If the trajectory violates obstacle clearance or appears infeasible, the system switches to the D* Lite fallback path.

The main pipeline is:

- Receive depth, semantic, and camera transform observations from the Isaac Sim environment. 
- Generate a candidate trajectory using ViPlanner.
- Convert depth observations into a local occupancy grid.
- Inflate detected obstacles to enforce a safety margin.
- Use D* Lite to compute a collision-aware fallback path.
- Check whether the ViPlanner path is safe.
- Execute the ViPlanner path if safe; otherwise switch to the D* Lite path.
- Convert the selected path into velocity commands for the Limo differential-drive robot.

The system also includes persistent obstacle memory. This allows previously observed obstacles to remain useful even after they leave the current camera field of view, which helps in partially observable environments.




## My Contributions

Early WSL+Ubuntu setup, high-speed computing hardware purveyor, Isaac-Sim Limo diff-drive exploration, Carla-map exploration, simulation vehicle testing, and ViPlanner demo testing and benchmarking.Contributed to simulation setup and testing for a CMU 18-744 autonomous navigation project using ViPlanner, Isaac Sim, and a Limo mobile robot platform.
Explored Isaac Sim/Limo differential-drive integration and CARLA-map compatibility during environment setup.
Ran ViPlanner demo testing and scenario benchmarking to evaluate planner behavior in blocked-road and obstacle-rich environments.
Helped validate a hybrid navigation system that reduced collision rate from 100% to 0% in wide-obstacle and complex narrow-passage scenarios, according to the team evaluation.

My specific responsibilities included early WSL/Ubuntu environment setup, hardware support for high-performance simulation, Isaac Sim and Limo robot exploration, CARLA map exploration, simulation vehicle testing, ViPlanner demo testing, and benchmarking support.

I contributed to the simulation and evaluation side of the project, helping the team identify practical environment issues, test the planner behavior in different obstacle scenarios, and validate whether the hybrid ViPlanner + D* Lite system improved safety compared with the baseline ViPlanner behavior.

I also helped document and communicate the system’s behavior, especially around simulation setup, planner testing, blocked-road scenarios, and benchmarking outcomes.

What tech stack did you use?

Tech stack: Python, C++, NVIDIA Isaac Sim, Isaac Lab, ViPlanner, D* Lite, ROS/robotics navigation concepts, occupancy grids, depth perception, semantic perception, Limo mobile robot simulation, WSL/Ubuntu, Linux, Git/GitHub, and high-performance GPU-based simulation.





## Results
The hybrid system preserved ViPlanner’s efficiency in simple environments while improving safety in harder scenarios. In the team evaluation, both baseline ViPlanner and the hybrid system achieved 0% collision rate and 100% success rate on clear-road and regular-obstacle scenarios.

In more challenging cases, the hybrid system performed better. In the wide-obstacle scenario, baseline ViPlanner had 100% collision rate and 0% success rate, while the hybrid system achieved 0% collision rate and 80% success rate. In the narrow-passage scenario, the hybrid system improved success rate from 40% to 100% while maintaining obstacle clearance. In the complex narrow-passage scenario, the hybrid system reduced collision rate from 100% to 0% and achieved 60% success rate.

These results suggest that adding a deterministic safety checker and D* Lite fallback planner can make a learning-based navigation system more reliable in blocked, narrow, or partially observable environments.


## Repository Notes
This is a portfolio repo, not the original upstream codebase.

(The source code in `code/viplanner/` is copied from our team development fork for portfolio and documentation purposes. This repository does not claim authorship of the original ViPlanner framework. The original upstream project and the team development fork are linked below.)

(This was a CMU team project. My individual contributions are listed above. Core implementation work was shared across the team, and the original development fork was maintained under my teammate’s GitHub account.)

## Links
- Development fork: https://github.com/JiaoZA01/viplanner
- Original ViPlanner: https://github.com/leggedrobotics/viplanner
- Final report: ./Final_744_Report_Documentation.pdf

(- Project source code in this portfolio repo: `code/viplanner/`)
(- Project media in this portfolio repo: `media/`)


## Media

### System Architecture
![System Architecture](media/system_architecture.png)

(Note: your uploaded file appears to be named `system_architecture.jpg`, so this image link should eventually be changed to `media/system_architecture.jpg` unless you rename the file to `system_architecture.png`.)

### Evaluation Results
![Evaluation Table](media/evaluation_table.png)

(Note: I do not currently see `evaluation_table.png` in your media folder. You can either upload a screenshot named `evaluation_table.png`, or replace this with a table written directly in Markdown.)

### Demo
![Navigation Demo](media/demo_navigation.gif)

(Note: your current demo files are `.mp4`, not `.gif`. GitHub Markdown usually links MP4 files better as normal links instead of image embeds. Example links can be added below.)

(Available demo videos:)

(- [D* Lite 50 Search Range](media/dlite50.mp4))  
(- [D* Lite 80 Search Range](media/dlite80.mp4))  
(- [D* Lite 120 Search Range](media/dlite120.mp4))  
(- [D* Lite Clear Scenario](media/dliteclear.mp4))  
(- [D* Lite Long Clear Scenario](media/dlitelongclear.mp4))  
(- [D* Lite Simple Scenario](media/dlitesimple.mp4))  
(- [Hybrid Blocked Field-of-View Scenario](media/hybridblockfov.mp4))  
(- [Hybrid Dense Obstacle Scenario](media/hybriddenser.mp4))  
(- [Hybrid Replanning Scenario](media/hybridreplanning.mp4))  
(- [Hybrid Safety Scenario](media/hybridsafety.mp4))  
(- [Narrow Passage Scenario](media/narrow.mp4))  
(- [ViPlanner Blocked Field-of-View Baseline](media/viplannerblockfov.mp4))  
(- [ViPlanner Dense Obstacle Baseline](media/viplannerdenser.mp4))


This repository is a portfolio summary of our CMU 18-744 course project. 
The original development fork was maintained by a teammate at JiaoZA01/viplanner. 
This repo summarizes the system, results, media, final report, and my contributions.

(This README is written to make the project easier for recruiters, classmates, and reviewers to understand without needing to inspect the full source code first.)
