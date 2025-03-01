# Face Detection,Encoding and Recognition

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


