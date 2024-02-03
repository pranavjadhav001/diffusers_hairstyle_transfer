# HairStyle Transfer using Diffusion
An attempt to solve hairstyle transfer problem using Diffusion using Diffusers pipeline for RePaint paper.<br/>
RePaint Paper link : https://arxiv.org/abs/2201.09865
This Repo has been forked from HuggingFace Diffusers and changes have been in RePaint Pipeline and scheduling scripts<br/>

## What has changed!

### Generating random hairstyles for face
Using Hairstyle_transfer_repaint_random.ipynb notebook, you can generate muliple hairstyles for a given face image. You can even generate more different cases by tweaking generator seed and eta parameter
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/random.png?raw=true)

### Hairstyle transfer from hair image to source image
Using Hairstyle_transfer_repaint.ipynb notebook, you can transfer hairstyle transfer from hair image to source(face) image. Repaint inference algorithm has been changed to make merge between face and hair boundary sublime and indistinguishable.Changes made are:
- Instead of starting from gaussian random noise image, we will take hair image and add image to about 50 steps
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/denoise_hair_image.png?raw=true)
- When harmonizing sampling begins, first instance of denoise step will allow addition of face
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/face_addition.png?raw=true)
- While the first adds face the rest of steps for reverse diffusion for that transition will only do denoising 
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/denoise.png?raw=true)
- For the section in harmonizing sampling where the noise is added to the image, remains the same.
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/noise.png?raw=true)
- After this harmonizing sampling period, there is addition of more steps consisting of noise and denoise in that order to further smoothen and gel the two images better.
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/image.png?raw=true)
-Transition/harmonizing Timeline
![alt text](https://github.com/pranavjadhav001/diffusers_hairstyle_transfer/blob/main/images/transition.png?raw=true)

### Areas to improve
Even though it works well for the above hair and source image. I've found instances of this approach not working well.<br/>
Reasons i suspect are:
- Alignment between hair and source image needs to be spot on.
- skin tone, if there is clear visible distinction the method fails, showing clear boundary between hair and face.

## Requirements
- Face Alignment
- Dlib 
- Opencv
- Diffusers
- Matplotlib
- Pillow
- Pytorch
- Numpy
