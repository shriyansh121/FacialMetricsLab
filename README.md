# Face Detection,Encoding and Triangulation

## Face Detection

### History of face detection

The first computerized face detection experiments were launched in 1964 by American mathematician Woodrow W. Bledsoe. His team at Panoramic Research in Palo Alto, Calif., used a rudimentary scanner to scan people's faces and find matches in an attempt to program computers to recognize faces. The experiment was largely unsuccessful because of the computer's difficulty with poses, lighting and facial expressions.

Major improvements to face detection methodology came in 2001 when computer vision researchers Paul Viola and Michael Jones at Mitsubishi Electric Research Laboratories proposed a framework to detect faces in real time with high accuracy.

The Viola-Jones algorithm trains a model to understand what is and is not a face. Once trained, the model extracts specific features and stores them in a file. Those features can be compared with the stored features at various stages. If the image under study passes through each stage of the feature comparison, then a face has been detected, and operations can proceed.

The Viola-Jones framework is still used to recognize faces in real-time applications, but it has limitations. For example, the framework might not work if a face is covered with a mask or scarf. In addition, if the face isn't properly oriented, the algorithm might not be able to find it. Recent years have brought advances in face detection using deep learning, which outperforms traditional computer vision methods.

### Popular Face Detection Software

Many software products and online services integrate face detection, each offering unique features and functionalities:

- Amazon Rekognition: A cloud-based service providing customizable computer vision capabilities, including real-time face detection and individual metadata pairing.
- Dlib: A C++ toolkit containing machine learning algorithms for complex software, including powerful face detection capabilities.
- Google Cloud Vision API: Provides APIs for advanced vision models, supporting basic face detection and identification in images and videos.
- Megvii AI: Deep learning-based face detection, designed to analyze complex and varied environments.
- Microsoft Face API: A cloud-based service offering face detection, verification, and grouping capabilities.
- OpenCV: An open-source computer vision library that supports real-time image processing, including object detection and face recognition.

For my face detection tasks, I chose to use OpenCV and Dlib. These two tools provide reliable and efficient methods for detecting faces in images. OpenCV is well-known for its simplicity and speed, making it a great choice for real-time image processing. Dlib, on the other hand, is particularly suited for more advanced and accurate face detection due to its powerful machine learning algorithms.

These libraries were chosen because of their ease of integration, reliability, and local processing capabilities, which suited my needs for face detection without the reliance on cloud-based services.

### Workflow  

#### Face Detection using DLIB
Dlib uses a machine learning-based approach to detect faces, primarily employing a pre-trained model known as the HOG (Histogram of Oriented Gradients) + SVM (Support Vector Machine) or a deep learning model for more accurate results. The face detection process begins by converting the image into grayscale to simplify the processing. Dlib’s face detector first identifies areas in the image that are likely to contain faces using the HOG feature descriptor. This descriptor analyzes the edges and gradients in an image, helping the algorithm detect regions where features like the nose, eyes, and mouth are present.

Once potential face regions are identified, the SVM classifier steps in to confirm whether the identified region is a face. The classifier is trained on positive and negative face samples, allowing it to distinguish between faces and non-faces. The result is a bounding box around the face with a high confidence score. Dlib also supports landmark detection which can identify key facial features (like eyes, nose, mouth) and even track facial landmarks across frames in videos. The deep learning-based model, while more computationally expensive, offers better performance for complex face detection tasks, such as recognizing faces in challenging lighting conditions or orientations.

#### Face Detection using HaarCascade
Haar Cascade is a classic method for face detection, implemented using Haar-like features in combination with a Cascade Classifier. The workflow starts by training the classifier using a large number of positive and negative image samples. Positive samples contain faces, while negative samples do not. The classifier is trained to detect features like edges, textures, and other patterns that are typically found around facial regions, such as the eyes, nose, and mouth.

The detection process begins by sliding a window across the input image at different scales. For each window, the Haar Cascade classifier computes various Haar features (like changes in intensity between adjacent regions) to identify whether the window contains a face. These features are summed up in the integral image to speed up the process. At each step, the classifier applies a series of weak classifiers, which are simple decision trees, to determine if a face is present or not.

Haar Cascades use a cascade of classifiers, meaning that only regions with a high likelihood of being faces are processed by more complex classifiers. This hierarchical approach allows the algorithm to discard non-face regions early on, improving efficiency. The result is a bounding box around the detected face. While Haar Cascade is faster and less computationally expensive than more modern methods, it can be less robust in challenging conditions like varying angles, lighting, or occlusions.

### Face Detection using Retinaface
RetinaFace is a type of face detection technology that uses a method called a convolutional neural network (CNN) to identify faces in images. It starts by adjusting the image size to suit the network while keeping the original shapes of features intact. RetinaFace uses a technique known as Feature Pyramid Network (FPN) which helps it to detect faces of different sizes, from very big to very small, by examining the image at multiple levels or scales.

The model also incorporates additional context to these features, which improves its ability to recognize faces that are partially hidden or smaller than usual. It performs several tasks at once—not only finding where the faces are but also estimating their size, identifying key facial points like the eyes and mouth, and sometimes even guessing gender.

For every face it detects, RetinaFace calculates a confidence score. This score tells how sure the model is that it has found a face. The process involves comparing the detected area with typical face features and deciding how likely it is to be a real face. The model uses a process called non-maximum suppression (NMS) to eliminate any redundant or overlapping detections, keeping only the most likely ones.

This multitasking approach, combined with its ability to handle images at multiple scales and incorporate contextual information, makes RetinaFace highly effective and accurate in detecting faces under a variety of challenging conditions.

### Face Detection using Yunet
YuNet is a compact and efficient face detection model designed to perform well on resource-constrained devices. The model employs a single-stage convolutional neural network (CNN) architecture, which is optimized for speed and low computational overhead. YuNet processes an input image through a series of convolutional layers, which extract features that are crucial for recognizing facial structures.

The core of YuNet’s efficiency lies in its use of depthwise separable convolutions, which significantly reduce the number of parameters without compromising the accuracy of face detection. This allows YuNet to detect faces quickly, even on devices with limited processing power. The model also incorporates a score regression mechanism to determine the likelihood of each detected area containing a face, enhancing the precision of its predictions.

Finally, YuNet applies a technique called non-maximum suppression (NMS) to refine the detection results. This step eliminates redundant detections and ensures that each face is only counted once, improving both the accuracy and reliability of the final output. Through these methods, YuNet achieves a balance of speed and accuracy, making it suitable for real-time face detection applications.

### Face Detection using MTCNN
MTCNN, or Multi-task Cascaded Convolutional Networks, is a robust and precise method for face detection that uses a three-stage deep learning framework. Each stage in MTCNN is designed to refine the detection progressively, focusing on different aspects of accuracy and bounding box adjustment.

In the first stage, called P-Net (Proposal Network), the model scans the entire image with a fully convolutional network to quickly propose candidate facial regions. It identifies potential faces and provides bounding box coordinates. It also predicts face probabilities which help in eliminating non-face regions early in the process.

Following P-Net, the second stage involves R-Net (Refinement Network), which takes the outputs from P-Net and refines these proposals. It helps to filter out a large number of false positives, refine the bounding boxes, and again outputs the likelihood of a face along with improved bounding box coordinates.

The final stage, O-Net (Output Network), provides the most refinement. O-Net further reduces false positives, fine-tunes the bounding box coordinates, and additionally provides facial landmarks (like the eyes, nose, and mouth positions). This detailed detection helps in accurately pinpointing facial features and orientations.

Throughout these stages, each network employs a technique called non-maximum suppression (NMS) to reduce overlap between bounding boxes, ensuring that each detected face is unique and clearly identified. This cascading approach allows MTCNN to detect faces with high accuracy and precision, making it effective even in complex visual environments with varying face orientations and scales.

### Result and Discussions




in dlib it cna only detect upto a specific number of images for more images compiled in single image dlib cannot detect it. also dlib in real time is slow. 
Haarcascade on other hand have a crazy accuracy and works on many faces in single images and also do not lag in real time making it more realiable than dlib.  

## Face Encoding

### Introduction to Face Encoding
Face encoding refers to the process of converting facial features into a numerical format that can be easily processed by machine learning algorithms. It’s a critical step in face recognition systems because it allows a system to recognize and compare faces by turning them into vectors or arrays of numbers. The key idea is to extract unique characteristics of a face that can be used for identification, matching, or verification.

### About Face Encoding
Face encoding works by analyzing various facial features such as the shape of the eyes, nose, mouth, and jawline. These features are then converted into a vector—a numerical representation— that captures the uniqueness of the face. When comparing faces, face encodings are compared using mathematical methods like Euclidean distance to determine similarity. The more similar the encoding, the more likely the faces belong to the same person.

### Types of Face Encoding

There are multiple methods to generate face encodings, and two popular ones are:

- Shape_predictor_68_face_landmarks (1).dat File Method (Dlib)
- Face Mesh Method (MediaPipe)

**1. Shape_predictor_68_face_landmarks (1).dat File Method (Dlib)**
   
![68 Facial Landmarks of Dlib](https://b2633864.smushcdn.com/2633864/wp-content/uploads/2017/04/facial_landmarks_68markup.jpg?lossy=2&strip=1&webp=1)

The shape_predictor_68_face_landmarks.dat file is a pre-trained model in Dlib used to detect 68 key facial landmarks on a face. These landmarks represent important features such as the eyes, eyebrows, nose, mouth, and jawline. Here's how this method works:

* Face Detection: First, the face is detected in the image or video using Dlib’s frontal face detector. This step produces a bounding box around the face, isolating the region of interest.

- Landmark Detection: The shape_predictor_68_face_landmarks.dat model is then applied to detect the 68 landmark points within the bounding box. These points include:
  * Eyes: 6 points for each eye (12 points total).
  * Eyebrows: 8 points (4 points per eyebrow).
  * Nose: 9 points, focusing on the tip of the nose and the nostrils.
  * Mouth: 20 points outlining the lips and corners of the mouth.
  * Jawline: 17 points along the jaw.

* Coordinate Calculation: The coordinates of these landmarks are expressed as pixel locations in the image. Dlib uses a regression model to predict these points based on the grayscale image of the face. Once the landmarks are identified, they can be used to create a geometric model of the face.

* Face Encoding: The 68 detected points are then converted into a vector. This vector captures the unique facial geometry, which can be used for face comparison. The distance between face encodings is used to determine the similarity between two faces.

**2. Face Mesh Method (MediaPipe)**

![468 Facial Landmarks of FaceMesh](https://cdn.analyticsvidhya.com/wp-content/uploads/2021/07/31127mesh_index_front.jpg)

The Face Mesh method by Google’s MediaPipe provides a more detailed and high-resolution model for detecting facial landmarks. It detects 468 facial landmarks rather than the 68 used by Dlib. This method is especially useful in scenarios requiring high precision, such as AR applications or detailed facial analysis.

* Face Detection: Similar to the Dlib method, the first step is detecting the face using MediaPipe’s face detection model. Once the face is located, the system proceeds to landmark detection.

* Landmark Detection: MediaPipe uses a deep learning-based model to detect 468 points on the face, including:

  * Eyes: Multiple points around each eye for more detailed contours.
  * Eyebrows: More precise control over the position and curvature of the eyebrows.
  * Nose, Mouth, and Jawline: Enhanced resolution with more points, providing a more detailed representation of facial features.

* Coordinate Calculation: The coordinates of these 468 points are calculated in a 3D space, giving more depth information compared to the 2D approach of Dlib. The points are typically normalized and mapped onto a 3D model of the face. The network behind the face mesh method uses a deep neural network to predict these coordinates.

* Face Encoding: After detecting and calculating the coordinates of the 468 landmarks, a face encoding can be created by transforming these points into a feature vector. This vector is more detailed and can be used to compare faces with a higher degree of precision.

### Conclusion
Both Dlib’s shape_predictor_68_face_landmarks.dat and MediaPipe’s Face Mesh method provide different approaches to face encoding, with Dlib focusing on a smaller set of landmarks for faster, more efficient recognition, and MediaPipe offering a more detailed and accurate model with 468 landmarks. Each method has its strengths depending on the application: Dlib is typically faster and requires less computation, while MediaPipe provides a higher level of detail and is suited for applications requiring precision, such as augmented reality.

### Result and Discussions

<img width="596" alt="Image" src="https://github.com/user-attachments/assets/a6de23cd-3ef0-452e-8451-1cb85ec20f4e" />
<img width="711" alt="Image" src="https://github.com/user-attachments/assets/c20800a9-e804-4e7a-b7ef-a4ee3fb38fdf" />
<img width="923" alt="Image" src="https://github.com/user-attachments/assets/517b1fa0-f85f-46bd-b875-6e449dd8d962" />
<img width="565" alt="Image" src="https://github.com/user-attachments/assets/637f4034-3198-4669-a68a-8ddc96407e82" />
[](https://github.com/shriyansh121/FacialMetricsLab/blob/7edbd422f1d8e027b3d7f5e7a423798cf3fa344e/results/Face%20Encodings/face_encoing_with_dlib.mov)
## Face Contour and Triangulation


### Result and Discussions

<img width="826" alt="Image" src="https://github.com/user-attachments/assets/e2db5770-42ce-4b26-a733-f80a4a196c74" /> 

[Real Time Face Contour](https://github.com/user-attachments/assets/5b846a07-0707-4815-8642-c5ce5cbe8faf)

<img width="584" alt="Image" src="https://github.com/user-attachments/assets/c426d7ed-866a-4f54-8e8c-9fcbc1b0f4b3" />
<img width="594" alt="Image" src="https://github.com/user-attachments/assets/bf76367a-729c-4910-b761-ff78da34616f" />
<img width="967" alt="Image" src="https://github.com/user-attachments/assets/63807871-f505-4060-951a-5bf742db42d4" />

Triangulation is best used when you need a detailed, structural understanding of a face for applications involving motion, 3D rendering, or where the physical dynamics of the face need to be closely simulated or tracked. This would be applicable in high-end security systems, advanced interactive systems like virtual reality, or detailed character animation in gaming and film.

Contour Detection is more suitable for applications that require basic shape recognition or when you need to segment or identify objects based on their outline. This could be used in automated inspection systems, basic facial recognition tasks, and applications where the focus is on identifying and differentiating objects based on their external boundaries rather than their internal or three-dimensional structure.







