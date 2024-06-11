# Using Rust for Playing Soccer With Robots at RoboCup

- [Talk Description at Conference Website](https://rustfest.ch/talks/using-rust-for-playing-soccer-with-robots-at-robocup/)

The goal of the RoboCup is to play humans vs. autonomous robots in soccer matches by the year 2050.
To drive progress toward this ambitious goal, annual competitions and conferences across various robotics sub-fields are held, to encourage research and development.
Traditionally, robot programming has been dominated by languages like C++ and Python.
However, first teams are adopting Rust for its benefits in safety, reliability, and performance.

In this talk, I will discuss our team's journey in transitioning from a C++ codebase to Rust.
Our full-stack codebase consists of a wide range of algorithms and applications designed for controlling autonomous robots.
These robots must execute tasks such as identifying the soccer ball, accurately determining their position on the field, strategizing their next moves, and executing actions like forward movement or ball kicking.
Our codebase includes several vision, behavioral, and motion algorithms paired with debugging applications.

Throughout the talk, I will share lessons learned from this transition process, touching not only on technical challenges but also on the education of our team members.

```
cargo install --git https://github.com/RazrFalcon/resvg --tag v0.41.0 resvg
cargo install --git https://github.com/typst/svg2pdf
```

- https://commons.wikimedia.org/wiki/File:RoboCup_Rescue_robot_Hector_from_Darmstadt_at_2010_German_open.jpg
- https://www.flickr.com/photos/robocup2013/9141117651
- https://www.flickr.com/photos/robocup2013/9143508922
- https://commons.wikimedia.org/wiki/File:RoboCup_2016_Leipzig_-_RoboCup_Logistics_League_%282%29.jpg
- https://commons.wikimedia.org/wiki/File:13-06-28-robocup-eindhoven-023.jpg
- https://commons.wikimedia.org/wiki/File:Small_size_robocup.jpg
- https://commons.wikimedia.org/wiki/File:RoboCup_2016_Leipzig_-_Humanoid_Kid_Size_League_(1).jpg
- https://commons.wikimedia.org/wiki/File:RoboCup-2D-Soccer-Simulation-Field.jpg
