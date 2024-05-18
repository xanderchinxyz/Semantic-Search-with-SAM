# Semantic Search With Segment Anything Model (SAM)

Basically using Meta's Segment Anything Model (SAM) in conjunction with OpenAI's Contrastive Language-Image Pretraining (CLIP) to improve semantic search specifically for a certain object in an image with many objects. I came up with this idea to better improve the semantic search capabilities for my ESP32-CAM semantic search wearable.

## Example Image:
<img src="https://github.com/xanderchinxyz/Semantic-Search-with-SAM/blob/main/assets/example_image.png" height="500"></img>

TEXT_DESCRIPTION = "black glasses frames"

## The Jist Of How It Works:
1. The SAM model segments the image into many sub-images based on the boundaries of the objects in an image
<br></br>
<img src="https://github.com/xanderchinxyz/Semantic-Search-with-SAM/blob/main/assets/segmented_images.png" height="300"></img>
<br></br>
3. A vector is generated for every sub-image using CLIP
4. A custom text description also embedded as a vector using CLIP
5. Cosine similarity between the text and each sub-image is calculated
6. Subimages with cosine similarities over a certain threshold will be outlined in a red rectangle in the final picture

<img src="https://github.com/xanderchinxyz/Semantic-Search-with-SAM/blob/main/assets/successful_object_outline.png" height="500"></img>

## Things To Note:
- The text description must be quite descriptive in order for the model to work well (describe the shape, color, and other visual characteristics of the object)
- This sometimes cannot perfectly outline the boundary of a specific object (thresholds and prompts will need to be adjusted for different images) - but it is great at identifying if an object is in an image.

Example with TEXT_DESCRIPTION = "a black oled screen with a blue boundary around it and a green tag on it":

<img src="https://github.com/xanderchinxyz/Semantic-Search-with-SAM/blob/main/assets/dual_outlines.png" height="500"></img>

- I used FastSAM instead of the larger SAM model because it's a lot faster (could be used for real-time use cases) and my computer kinda sucks.
- I know FastSAM kind of already does this (it has a text prompt option to mask a specific object in an image) but it always masks something in the image even if it is wrong. I couldn't figure out how to get the cosine similarity score of the object mask compared to the text description it is given to prevent it from masking anything in the image if the score is too low

# Installation
1. Clone this git repo
2. Install required libraries in requirements.txt
3. Download the FastSAM-x.pt model from here: https://drive.google.com/file/d/1m1sjY4ihXBU1fZXdQ-Xdj-mDltW-2Rqv/view and put it in the main directory
