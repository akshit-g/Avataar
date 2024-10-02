# Pose Editing Using Generative AI

This repository provides a solution for object pose-editing based on generative AI techniques like CLIP, SAM, Zero123 (for 3D object generation), EDSR (for image enhancement), and Stable Diffusion inpainting. The project focuses on rotating an object in a given image while preserving the background.

## Features
- **Object Segmentation**: Uses CLIP + SAM to identify and segment objects from the image based on a text prompt.
- **Pose Editing**: Uses Zero123 to edit the pose of the segmented object by adjusting azimuth and polar angles.
- **Image Enhancement**: Utilizes EDSR to enhance the object’s resolution.
- **Background Reconstruction**: Applies Stable Diffusion inpainting to reconstruct the background after the object has been moved.
- **Compositing**: Combines the enhanced object back into the inpainted background.



# Pose Editing Project: Report

## Overview

This project required me to manipulate the pose of an object in an image while keeping the background unchanged. The process involved a series of generative AI models, and I iteratively worked through multiple challenges to come up with a solution. It was my first time working with 3D object generation and Stable Diffusion, which resulted in many failures, but ultimately a very enriching learning experience.

## Approach

### Step-by-Step Process:

1. **CLIP + SAM**: 
   - I used CLIP to identify the region of the object based on a text prompt and SAM to segment the object. Initially, aligning the prompt to the object proved difficult as CLIP misidentified certain objects or generated too large regions.
   
   **Failures**: In early attempts, the segmentation didn’t always match the object. For example, a prompt for "chair" would sometimes misidentify nearby objects with similar textures. This was improved, but it still malfunctions.

2. **Pose Editing with Zero123**: 
   - Zero123 was used to adjust the object’s pose. The transformation worked well for small rotations, but larger angles often led to unrealistic shapes.

   **Failures**: A 90-degree azimuth shift caused distortions, and small objects would often become too blurry. I iterated by experimenting with different angles and adjusting prompts to make the object stand out better in 3D.

3. **Image Enhancement with EDSR**: 
   - To improve image quality, I tried to use the EDSR model to upscale the image. While the upscaling worked at times, it sometimes introduced artifacts, especially in complex shapes. This was removed.

   **Failures**: Initial attempts resulted in poor upscaling of the object’s edges.

4. **Background Inpainting**: 
   - Using Stable Diffusion for background inpainting was a critical step. Initially, I struggled with setting up the model correctly and configuring the mask dilation.

   **Failures**: Inpainting produced unnatural backgrounds in cases where the object size was large, leading to mismatched textures. I mitigated this by fine-tuning the dilation mask and using smaller pose changes.

5. **Compositing the Image**: 
   - After creating the rotated object and the inpainted background, I composited the two using OpenCV.

   **Failures**: Aligning the object perfectly to the original coordinates in the composite image was tricky. 


## Analysis of Successes and Failures

### Successes:
- The integration of various generative models like CLIP, SAM, and Zero123 allowed for a flexible solution to the problem.
- Smaller pose edits (like +30 azimuth) resulted in realistic outputs that preserved the object's integrity.

### Failures:
- Larger pose shifts led to unrealistic objects due to limitations in Zero123’s generation.
- Upscaling didn’t always maintain fine details in complex objects.
- Background inpainting occasionally mismatched the texture of the original background, leading to discontinuities in some parts of the image.
- EDSR did not give the expected result.
- The SAM still has issues and is unable to segemnt the objects properly
- Zero123 stopped working and is unable to create the images now.

### Improvements and Future Work:
- Fine-tuning Zero123 to work better with large azimuth/polar shifts would improve the output for larger rotations.
- Experimenting with alternative enhancement techniques alongside EDSR might help reduce artifacts.
- For more complex scenes, training Stable Diffusion with additional prompts to improve texture matching in inpainting could enhance background reconstruction.
- Making the Zero123 work again and debugging the errors.

## Conclusion
This project was an incredible learning experience. I had never worked with 3D object generation or Stable Diffusion before, and the multiple iterations and failures taught me a lot about generative models. While the results are not perfect, this journey helped me explore new concepts and identify areas for improvement. I look forward to refining this project and applying similar techniques in future AI-based tasks.