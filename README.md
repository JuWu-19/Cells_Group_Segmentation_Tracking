# Pseudomonas aeruginosa Cell Group Segmentation and Motion Analysis

## Introduction

This repository contains the code and analysis in jupyter notebook for studying the motion of Pseudomonas aeruginosa, a bacterium known for its role in various infections. The purpose of this analysis is to gain insights into the movement patterns of these bacteria using two distinct computational approaches: Computational Fluid Dynamics (CFD)-inspired analysis and Agent-based Particle Tracking. These methods provide a comprehensive understanding of bacterial behaviors under different conditions.

## Segmentation Method: Adaptive Threshold Contour Detection

### Description

First the segmentation of bacteria images is achieved through adaptive threshold contour detection to separate the individual bacteria cells from the background of the microscope images. This method involves:

- **Adaptive Edge Detection**: The image is divided into smaller blocks, and edge detection is performed adaptively on each block. This approach accounts for local variations in lighting and texture.
- **Threshold Setting**: For each block, the threshold for edge detection is set based on the median pixel value within the block, adjusted by a proportion (`sigma`). This ensures that the edge detection is sensitive to the specific characteristics of each block.
- **Canny Edge Detection**: The Canny edge detection algorithm is applied to each block using the calculated thresholds, effectively highlighting the edges of bacteria.
- **Result Compilation**: The detected edges from all blocks are compiled into a single image, providing a comprehensive view of the bacteria contours.

This method is particularly effective in handling images with varying illumination and contrast, ensuring accurate detection of bacterial boundaries, the segmentation for one of images in the experiment pilG_dilute_PC is shown as follows, as you can see the edges for the bacteria cells are red:

<table>
  <tr>
    <td><img src="https://github.com/JuWu-19/Cells_Group_Segmentation_Tracking/assets/58901415/52c744d2-3558-4ece-bc9b-43b53b1c31f2" width="78%"/></td>
    <td><img src="https://github.com/JuWu-19/Cells_Group_Segmentation_Tracking/assets/58901415/b3b48b4a-ea77-498e-88d4-547959d7d8ed" width="78%"/></td>
  </tr>
  <tr>
    <td align="center">pilG_dilute_PC</td>
    <td align="center">Segmented Image</td>
  </tr>
</table>

## Method 1: CFD-Inspired Analysis

### Features and Functionalities

- **Density Field Calculation**: For each frame, the density of bacteria in local regions is computed using a grid overlay on the image. The density is calculated as the number of black pixels (representing bacteria) in each grid cell.
- **Velocity Field Calculation**: By comparing the density fields of consecutive frames, the movement of bacteria is estimated. The displacement of bacteria between frames, divided by the time step, gives the velocity.
- **Visualization**: The density and velocity fields are visualized using heatmaps or vector plots, providing an intuitive understanding of bacterial movement.
- **Analysis**: The velocity and density fields are analyzed to study collective behaviors, such as clustering, dispersion, or flow patterns.

The animations are too big to upload, so the snapshots of the heatmap animations for the microscope images in the experiment pilG_dilute_PC and pilG_dense_PC are as follows:
<table>
  <tr>
    <td><img src="https://github.com/JuWu-19/Cells_Group_Segmentation_Tracking/assets/58901415/afbc95a1-15a4-4dff-8aed-023545801358" width="78%"/></td>
    <td><img src="https://github.com/JuWu-19/Cells_Group_Segmentation_Tracking/assets/58901415/81f7c2f4-909e-47d1-92af-34aa857d2223" width="78%"/></td>
  </tr>
  <tr>
    <td align="center">Density heatmap for pilG_dense_PC</td>
    <td align="center">Velocity heatmap for pilG_dilute_PC</td>
  </tr>
</table>

## Method 2: Agent-Based Particle Tracking

### Features and Functionalities

- **Feature Extraction**: For each detected bacterium, features such as centroid, area, aspect ratio, solidity, perimeter, and circularity are computed.
- **ID Assignment**: Unique IDs are assigned to each detected bacterium in the first frame, and these are stored in a data structure.
- **Tracking Across Frames**: Bacteria are tracked across frames by comparing features and locations. A distance metric is used to measure the similarity between bacteria in consecutive frames.
- **Handling Merging and Splitting**: The algorithm accounts for scenarios where bacteria might merge into a single blob or split into multiple entities.
- **Result Storage**: The ID, features, and location of each bacterium are stored for each frame, facilitating further analysis and visualization.

### Implementation

The Agent-based Particle Tracking is implemented in *class BacteriaTracker*. It involves contour detection, feature extraction, and the application of tracking algorithms to follow the movement of each bacterium across multiple frames. The animations are too big to upload, so the snapshots of the specific timesteps of the animations for the microscope images in the experiment pilG_dilute_PC are as follows:
<table>
  <tr>
    <td><img src="https://github.com/JuWu-19/Cells_Group_Segmentation_Tracking/assets/58901415/fcfbfd90-265f-4f0f-9504-8487f751fe92" width="88%"/></td>
    <td><img src="https://github.com/JuWu-19/Cells_Group_Segmentation_Tracking/assets/58901415/783876c3-600b-402c-977e-844984099f9b" width="88%"/></td>
  </tr>
  <tr>
    <td align="center">Time step 0</td>
    <td align="center">Time step 4</td>
  </tr>
</table>

## Limitations and Outlook

- **Template Matching Limitations**: The template matching approach does not account for shape variance among bacteria. This limitation led to the development of edge and contour detection-based segmentation methods.
- **Data-Driven Feature Learning**: Manually annotated data could enhance bacteria identification. The binary images currently used are not suitable for object detection as they lose valuable information, particularly the texture of cells.
- **Bacteria Behavior Modeling**: Bacteria and other cells are not intelligent agents but conform to specific sets of behavior rules. Their dynamic mechanisms can be constructed to facilitate object tracking.
  - **Improved Tracking**: The current method of mapping cell IDs between frames is based on centroid distance and geometric feature similarity. New similarity features need to be proposed, along with predictive tracking based on simplified dynamics, to identify and track each unique cell across frames.
- **Handling Complex Cell Behaviors**: Conditions such as cell fission, overlapping, moving out of the window, and returning need to be considered to enhance the robustness of cell identification and tracking. The Optical Flow method will be explored in future work.
- **Optimization for Visualization**: The visualization process (making and storing the media) requires significant RAM. Tracking and identification algorithms can be optimized to save both time and space, making the process more efficient.

These limitations highlight areas for future development and improvement, suggesting a roadmap for advancing the study of bacterial motion analysis.
