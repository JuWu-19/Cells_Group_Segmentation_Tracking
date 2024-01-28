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
    <td><img src="https://private-user-images.githubusercontent.com/58901415/300183851-8e761e12-cfa5-429c-bd47-69bf00bfc57d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDYzNjU2NTUsIm5iZiI6MTcwNjM2NTM1NSwicGF0aCI6Ii81ODkwMTQxNS8zMDAxODM4NTEtOGU3NjFlMTItY2ZhNS00MjljLWJkNDctNjliZjAwYmZjNTdkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMjclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTI3VDE0MjIzNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ5YzBlYzc5ZWQ5YjdhOTk3YzY2MDMxMGY0MDQyZDFlNzQ3NzZjOTgyZTNlMGM1MzJhYjI5YmJmYWUyODkzYWImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.UgmWvjX5ej-LHAKGEgrN-lqRoqt3zTFQDvB-PyzM4q0" width="78%"/></td>
    <td><img src="https://private-user-images.githubusercontent.com/58901415/300184371-9c155cac-4c9d-4bf6-bd5f-219d68c9bb8a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDYzNjYxNzUsIm5iZiI6MTcwNjM2NTg3NSwicGF0aCI6Ii81ODkwMTQxNS8zMDAxODQzNzEtOWMxNTVjYWMtNGM5ZC00YmY2LWJkNWYtMjE5ZDY4YzliYjhhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMjclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTI3VDE0MzExNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTA1YmMzYzUyNzZjYWY5MjZhN2VmN2M2Zjk1YWZiYmNkMTM0MWI2NWE3YzVmODk3MWYzODkxNzZmM2IyNDhjN2QmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.oTCkcWaPt0CamWhx5ZNhr6dv4r5r5D9gbaXAHkGb4TI" width="78%"/></td>
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

The animations are too big to upload, so the snapshots for the heatmap animations are as follows:
<table>
  <tr>
    <td><img src="https://private-user-images.githubusercontent.com/58901415/300183851-8e761e12-cfa5-429c-bd47-69bf00bfc57d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDYzNjU2NTUsIm5iZiI6MTcwNjM2NTM1NSwicGF0aCI6Ii81ODkwMTQxNS8zMDAxODM4NTEtOGU3NjFlMTItY2ZhNS00MjljLWJkNDctNjliZjAwYmZjNTdkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMjclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTI3VDE0MjIzNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ5YzBlYzc5ZWQ5YjdhOTk3YzY2MDMxMGY0MDQyZDFlNzQ3NzZjOTgyZTNlMGM1MzJhYjI5YmJmYWUyODkzYWImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.UgmWvjX5ej-LHAKGEgrN-lqRoqt3zTFQDvB-PyzM4q0" width="78%"/></td>
    <td><img src="https://private-user-images.githubusercontent.com/58901415/300184371-9c155cac-4c9d-4bf6-bd5f-219d68c9bb8a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDYzNjYxNzUsIm5iZiI6MTcwNjM2NTg3NSwicGF0aCI6Ii81ODkwMTQxNS8zMDAxODQzNzEtOWMxNTVjYWMtNGM5ZC00YmY2LWJkNWYtMjE5ZDY4YzliYjhhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMjclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTI3VDE0MzExNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTA1YmMzYzUyNzZjYWY5MjZhN2VmN2M2Zjk1YWZiYmNkMTM0MWI2NWE3YzVmODk3MWYzODkxNzZmM2IyNDhjN2QmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.oTCkcWaPt0CamWhx5ZNhr6dv4r5r5D9gbaXAHkGb4TI" width="78%"/></td>
  </tr>
  <tr>
    <td align="center">pilG_dilute_PC</td>
    <td align="center">Segmented Image</td>
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

The Agent-based Particle Tracking is implemented in *class BacteriaTracker*. It involves contour detection, feature extraction, and the application of tracking algorithms to follow the movement of each bacterium across multiple frames.

### Cases

- **Case 1**: Tracking of bacteria in a static environment, highlighting individual trajectories.
  - Media: Two images showing the initial and final positions of bacteria with trajectory lines.
- **Case 2**: Dynamic tracking of bacteria over time, with visualization of changing positions and paths.
  - Media: 
    - Image showing the initial positions and IDs of bacteria.
    - GIF animation illustrating the movement and trajectories of bacteria over time.
   
## Limitations and Outlook

- **Template Matching Limitations**: The template matching approach does not account for shape variance among bacteria. This limitation led to the development of edge and contour detection-based segmentation methods.
- **Data-Driven Feature Learning**: Manually annotated data could enhance bacteria identification. The binary images currently used are not suitable for object detection as they lose valuable information, particularly the texture of cells.
- **Bacteria Behavior Modeling**: Bacteria and other cells are not intelligent agents but conform to specific sets of behavior rules. Their dynamic mechanisms can be constructed to facilitate object tracking.
  - **Improved Tracking**: The current method of mapping cell IDs between frames is based on centroid distance and geometric feature similarity. New similarity features need to be proposed, along with predictive tracking based on simplified dynamics, to identify and track each unique cell across frames.
- **Handling Complex Cell Behaviors**: Conditions such as cell fission, overlapping, moving out of the window, and returning need to be considered to enhance the robustness of cell identification and tracking. The Optical Flow method will be explored in future work.
- **Optimization for Visualization**: The visualization process requires significant RAM. Tracking and identification algorithms can be optimized to save both time and space, making the process more efficient.

These limitations highlight areas for future development and improvement, suggesting a roadmap for advancing the study of bacterial motion analysis.
