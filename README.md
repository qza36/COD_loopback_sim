# Nav2 LoopBack Sim
This project was created using RoboStack.

A lightweight testing environment designed for rapidly validating algorithms and converting them into Nav2 plugins.

Using Gazebo for initial path planning and control testing can be unnecessarily cumbersome. It forces developers to contend with physics-engine artifacts—such as odometry drift and positioning errors—which are distractions at this stage. Loopback isolates the control logic, allowing us to focus purely on algorithm verification before transitioning to high-fidelity simulations.

## Motivation

The official nav2_loopback_sim is readily available for Jazzy. However, since it hasn't been backported to the Humble apt sources yet, I created this standalone integration to provide equivalent functionality on Humble.

<details><summary><b>Why RoboStack & Pixi? (Click to expand)</b></summary>
Developing on a MacBook, I wanted a native ROS2 experience (using Rviz, RQT, etc.) without the heavy disk footprint and overhead of Docker. To achieve this, I chose RoboStack, managed via Pixi, to construct a lightweight environment.

This setup proved perfect for my current research into path planning and control. It offers a compact workflow that allows me to test algorithms efficiently, completely avoiding the resource intensity and installation pitfalls often associated with Gazebo.
</details>

## Prerequisites
- pixi<br>
```bash
curl -fsSL https://pixi.sh/install.sh | bash
```
## How to run 
- clone this project 
```bash
pixi install
pixi run build
```
> [!WARNING] Do not use --symlink-install. Using symlinks currently causes nav2_loopback_sim to encounter errors during compilation.

- launch the loopback simulation (will auto-build before launching). The sim includes `nav2_route`'s route_server with the turtlebot3 graph.
```bash
pixi run sim
```

- launch the loopback simulation with a route-focused rviz view (shows route graph and waypoint markers)
```bash
pixi run route
```

- launch the standalone route editing tool (rviz2 + map_server, no simulation). Use this to create or edit `.geojson` route graph files.
```bash
pixi run route_tool
```
You can also specify a different map file:
```bash
pixi run bash -c 'source install/setup.bash && ros2 launch nav2_rviz_plugins route_tool.launch.py yaml_filename:=/path/to/your/map.yaml'
```
