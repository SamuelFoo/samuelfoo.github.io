---
title: "Particle Filtering & Potential Fields for Rescue Autonomy"
excerpt: >
  <div class="media-row--sm">
    <img src="/images/projects/rcap/particle_filter.gif" style="width: auto; height: 200px;"/>
    <img src="/images/projects/rcap/repulsion_vectors.svg" style="width: auto; height: 200px;"/>
  </div>
collection: projects
---

Virtual RoboCup CoSpace Rescue is a competition where virtual robots are programmed to autonomously search for and deliver objects in a semi-dynamic environment. To win the competition, I obtained much more precise localization compared to my peers by considering terrain features and used artificial potential fields to allow for smooth object avoidance while having reactive control.

Here is a video of my finals run:

<iframe width="560" height="315" src="https://www.youtube.com/embed/mC7l_4lkLTw?si=BhQF01gGnapT_2iT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

## Localization using Particle Filters

The robot is equipped with three front-facing ultrasonic sensors. First, we calibrate the sensors to a common reference point.

<div class="media-row--sm">
    <img src="/images/projects/rcap/calibration.svg"/>
</div>
<br>

From an image of the map, the obstacles were segmented out and used to predict expected ultrasonic readings at candidate poses.

<div class="media-row--sm">
    <img src="/images/projects/rcap/map.png"/>
    <img src="/images/projects/rcap/map_with_obstacles.png"/>
</div>
<br>

This was represented as a set of distance maps at different bearings.

<div class="media-row--sm">
    <img src="/images/projects/rcap/distance_maps.svg"/>
</div>
<br>

By intersecting the feasible sets implied by the robot's ultrasonic sensors and its bearing, we can narrow the robot's position to a few possibilities.

<div class="media-row--sm">
    <img src="/images/projects/rcap/possible_positions.svg"/>
</div>
<br>

Finally, a particle filter uses information from past readings to give us the final correct pose.

<div class="media-row--sm">
    <img src="/images/projects/rcap/particle_filter.gif"/>
</div>
<br>

## Artificial Potential Fields

The map can also be used to enhance path-planning to allow for smooth object avoidance while having reactive control.

A strong "repulsive" wall-avoidance term, that grows rapidly as the robot gets close to obstacles, was blended with a "goal-seeking" targeting steer so the robot can keep making progress toward a target grid without hugging walls or colliding. 

<div class="media-row--sm">
    <img src="/images/projects/rcap/repulsion_vectors.svg"/>
    <img src="/images/projects/rcap/obstacle_avoidance.gif"/>
</div>
