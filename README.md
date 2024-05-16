# Semantic Search With Segment Anything Model (SAM)

Basically using Meta's Segment Anything Model (SAM) in conjunction with OpenAI's Contrastive Language-Image Pretraining (CLIP) to improve semantic search specifically for a certain object in an image with many objects. I came up with this idea to better improve the semantic search capabilities for my ESP32-CAM semantic search wearable

For each image:
1. The SAM model segments the image into many subimages based around the boundaries of the objects in an image
2. A vector is generated for every subimage using CLIP
3. A custom text description also embedded as a vector using CLIP
4. Cosine similarity between the text and each subimage is calculated
5. Subimages with cosine similarities over a certain threshold will be outlined in a red rectangle in the final picture

## Things to note:
- The text description must be quite descriptive in order for the model to work well (describe the shape, color, and other visual characteristics of the object)
- This sometimes cannot perfectly outline the boundary of a specific object (thresholds and prompts will need to be adjusted for different images) - but it is great at identifying if an object is in an image
- I used FastSAM instead of the larger SAM model because it's a lot faster (could be used for real-time usecases) and my computer kinda sucks.
- I know FastSAM kind of already does this (it has a text prompt option to mask a specific object in an image) but it always masks something in the image even if it is wrong. I couldn't figure out how to get the cosine similarity score of the object mask compared to the text description it is given to prevent it from masking anything in the image if the score is too low