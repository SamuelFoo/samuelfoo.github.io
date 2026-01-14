---
title: "RoboSub 2025"
excerpt: >
  <div class="media-row--sm">
    <img src="/images/projects/robosub/torpedo_preview.gif" style="width: auto; height: 200px;"/>
    <img src="/images/projects/robosub/trash_preview.gif" style="width: auto; height: 200px;"/>
  </div>
collection: projects
---

[RoboSub](https://robosub.org/programs/2025/) is an international competition that invites participants to tackle simplified versions of challenges facing the underwater maritime industry. These challenges may include oceanographic exploration and mapping, detection and manipulation of objects, and pipeline identification and tracking.

## Bin

<div class="media-row">
  <img src="/images/projects/robosub/bin_success_yolo_cropped.gif" />
  <img src="/images/projects/robosub/bin_correcting_template_cropped.gif" />
</div>
<br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Tc7IWZhyndc?si=RzgBFvt_XzempjSB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

**Task:** The AUV is to drop two markers on the half of the bin corresponding to a specified animal.

**Main Challenge:** Detection of the bin image is challenging in harsh lighting.

**Our Approach:** From far away, detect the bin image using YOLO as the images of the animals aren't clear enough for feature matching to work. However, pose estimation of the non-square quadrilateral leaves a 180 deg ambiguity. We disambiguate by counting the number of point correspondences with the un-rotated and rotated templates. Then, Perspective-n-Point (PnP) on the point correspondences gives us the 6-DoF poses of the centers of the animals.

<img src="/images/projects/robosub/bin_transforms.png" />

## Slalom

<iframe width="560" height="315" src="https://www.youtube.com/embed/s_MKozIs_Lc?si=aK1NtuUlS-kSPd-C" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

**Task:** The AUV is to navigate the channel of white and red vertical PVC pipes while staying on the same side of the red pipe when it passed through the gate (i.e., if the AUV passed on the right of the red gate divider, it should pass through the Slalom with the red pipe on the right).

**Main Challenge:** Determining which poles belong to which layer is difficult as our robot lacks depth perception. Matching poles to wrong layers would cause the poses of the layers to be estimated wrongly.

**Our Approach:** In deciding whether a white pole is in the same layer as a red pole, we computed a "similarity score" based on how close their relative depth values and the heights of their oriented bounding boxes are. The relative depth values are obtained from a monocular depth model.

## Torpedoes

<iframe width="560" height="315" src="https://www.youtube.com/embed/EO9MKfeytO8?si=YLRtqYJCKmFivYx0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

**Task:** The AUV is to detect the animals on the target and "tag" them in a specified order by firing torpedoes through the respective openings. More points are awarded for firing far from the target.

**Main Challenge:** Due to limitations on the firing power of our "torpedoes" (spring-propelled projectiles), we often fire from positions where the target is partially occluded. This makes it challenging to locate the holes.

**Our Approach:** We use feature matching to generate point correspondences for PnP. This allows us to determine both the location of the holes and the animal they represent while being robust to occlusions. Notably, this approach doesn't require prior training data and is generalizable to any target (most teams require object detection models to detect the shark, fish and the holes, ours doesn't). Furthermore, by detecting the 6-DoF pose of the board (with a precision of ~3 cm and ~1 deg), we are able to fire in a direction orthogonal to the plane containing the holes, maximizing our chances of success. (Fun fact: we used the orientation of the torpedo target to correct for IMU drift during our finals run.)

## Ocean Cleanup

<iframe width="560" height="315" src="https://www.youtube.com/embed/xBKHFBSmb50?si=9gi5RQWe7AKFyd8w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

**Task:** The AUV is to sort objects into baskets of opposing colors. After picking up each sample, it must surface before depositing it.

**Main Challenge:** We do not have good odometry near the table due to the limitations of our doppler velocity log (DVL). The objects appear very differently at different depths, making tracking and pose estimation difficult.

**Our Approach:** By estimating the pose of the table and assuming that the objects are at the same depth as the table, we are able to determine the 6-DoF poses of the objects from their back-projections. We make use of a well-tuned multi-object tracker so that the target would not jump between multiple instances of the same object. Position-based visual servoing was used when the DVL becomes noisy near the table.
