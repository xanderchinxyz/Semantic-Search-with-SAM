Basically using Meta's Segment Anything Model (SAM) in conjunction with OpenAI's Contrastive Language-Image Pretraining (CLIP) to improve semantic search specifically for a certain object in an image with many objects

For each image:
1. The SAM model segments the image into many subimages based around the boundaries of the objects in an image
2. A vector is generated for every subimage using CLIP
3. A custom text description also embedded as a vector using CLIP
4. Cosine similarity between the text and each subimage is calculated
5. Subimages with cosine similarities over a certain threshold will be outlined in red in the final picture
