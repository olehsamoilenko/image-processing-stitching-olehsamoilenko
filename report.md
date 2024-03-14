## My approach:
1. Take 3 images
2. I would like the central image to remain unchanged, but warp left and right images into the perspective of the central image
2. Find keypoints in all 3 images using SIFT algorithm
3. Match keypoints of central image with:
     - keypoints of left image
     - keypoints of the right image
4. Find the homography using RANSAC algorithm:
     - between keypoints of central and left image
     - between keypoints of central and right image
5. Warp left and right images with obtained homographies
6. Throw everything together

## Challenges:
1. ~~I did not find a way to correctly place the central image (original) next to the left one (warped). That's why the central image is extended at the beginning to have some space for warped images to be placed.~~ Solved. I shifted destination keypoints for left and right images, no need to extend central image.<br>
2. I warped both images (left and right ones) to the perspective of the central one. Maybe it is better to stitch 2 images, recalculate keypoints and then stitch with the 3rd one.
3. At the final output central image is almost fully covered by 2 warped images. Looks like the central image is redundant in this case, and stitching only 2 images (left and right) would give the same result.
4. The final result is not ideal: in the right lower corner we see a pillar that was stitched incorrectly. Inscreasing number of keypoints does not solve the problem.

## TODO (if I have time):
1. ~~RGB~~<br>
2. Retake central image (avoid full covering by other images)