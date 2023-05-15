# Face recognition using Eigenfaces

## Abstract
This project was based on Turk and Pentland's research paper, "Face Recognition using Eigenfaces." We followed their methodology and implemented it by utilizing basic algebra functions from the Numpy library. The project involved several steps, including image preprocessing, construction of eigenfaces, representing images in the eigenspace, face recognition using the K-nearest neighbors (KNN) algorithm, and evaluating the performance of the system.

To evaluate the performance, we used the ATT face dataset, previously known as "The ORL Database of Faces".

## Dataset:
### AT&T "The Database of Faces" (formerly "The ORL Database of Faces")
Ten different images of each of 40 distinct subjects. The images were taken at different times, varying the lighting, facial expressions (open / closed eyes, smiling / not smiling) and facial details (glasses / no glasses). All the images were taken against a dark homogeneous background with the subjects in an upright, frontal position (with tolerance for some side movement)

### Methodology, Workflow and Result
1.	Load images and convert every of them into a Numpy matrix xi;
2.	Compute the mean:  

Figure 1 Mean image  
![Figure 1 AT&T database mean image](/result/att_mean_image.png?raw=true "AT&T database mean image")

3.	Compute the normalized images:

4.	Compute the ¡°Covariance Matrix¡± S, which is a modified version of the covariance matrix designed to mitigate issues related to large matrices during eigen decomposition:

5.	Compute the eigenvalue and eigenvector

Figure 3 Percentage of variance for each eigenvector
![result](/result/att_variance_distribution.png?raw=true)

Figure 5 Top 16 eigenfaces
![result](/result/att_top_16_eigenfaces.png?raw=true)

6.	Project an image into eigenspace and reconstruct using K eigenfaces:
W = vTXi  
Xf = V W  

Figure 7 Reconstruct using 80% variance
![result](/result/att_var080_faces43.png?raw=true)

Figure 8 Reconstruct using 90% variance
![result](/result/att_var090_faces110.png?raw=true)

Figure 9 Reconstruct using 95% variance
![result](/result/att_var095_faces189.png?raw=true)

Figure 10 Reconstruct using 99% variance
![result](/result/att_var099_faces324.png?raw=true)

7.	Recognition
In this image recognition approach, we used a technique called eigenface projection. By projecting an image onto a set of eigenfaces, we represented the image as a combination of these eigenfaces. The weights associated with the eigenfaces represented the image itself. To reduce the dimensionality, we only considered the top n eigenfaces, determined by the amount of variance they can capture. We examined four variance thresholds: 99%, 95%, 90%, and 80%. For the two datasets, the corresponding values of n were 324, 189, 180, and 43, respectively.

To recognize an unknown face, we employed the K-nearest neighbors (KNN) algorithm. We treated each image in the dataset as a query image and used the remaining images as training data. By finding the K nearest neighbors, we allowed them to vote and determine the label for the query image. In case of a tie, we chose the label with the least average distance.

To evaluate the performance of the recognition system, we assessed the precision, which was calculated based on the predicted label and the ground truth label. If the predicted label matched the ground truth label, it was considered a true positive; otherwise, it was a false positive.

Furthermore, we explored different values of k in the KNN algorithm, ranging from 1 to 10, to analyze its impact on the recognition accuracy.

Figure 15 Precisions for different k neighbors and n percent of variances
![result](/result/att_precision.png?raw=true)

## Reference:
* Turk, Matthew A., and Alex P. Pentland. "Face recognition using eigenfaces." Computer Vision and Pattern Recognition, 1991. Proceedings CVPR'91., IEEE Computer Society Conference on. IEEE, 1991.
* Turk, Matthew, and Alex Pentland. "Eigenfaces for recognition." Journal of cognitive neuroscience 3.1 (1991): 71-86.
* Belhumeur, Peter N., Jo?o P. Hespanha, and David J. Kriegman. "Eigenfaces vs. fisherfaces: Recognition using class specific linear projection." IEEE Transactions on pattern analysis and machine intelligence 19.7 (1997): 711-720.
* http://www.cl.cam.ac.uk/research/dtg/attarchive/facedatabase.html
* Belhumeur, Peter N., Jo?o P. Hespanha, and David J. Kriegman. "Eigenfaces vs. fisherfaces: Recognition using class specific linear projection." IEEE Transactions on pattern analysis and machine intelligence 19.7 (1997): 711-720.
