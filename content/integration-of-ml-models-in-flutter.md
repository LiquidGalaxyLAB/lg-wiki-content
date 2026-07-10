---
title: Integration of ML models in Flutter
contributor: Aritra Biswas
date: 2024-06-05T14:21:42.332+00:00
---

Machine Learning and Artificial Intelligence has taken the world by storm. It has affected every sector, and of course, App Development is no exception. AI/ML brings with it the potential to revolutionize the way our apps work. So, ML model integration has become a critical part of app development.  
  
TensorFlowLite \[TFLite\] is a highly intuitive framework that allows easy integration of ML models in our Flutter app.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Training an ML model:**
-------------------------

TensorFlow Lite is an extremely useful resource for ML model integration in Flutter. It provides an extensive array of pre-trained models ranging from object detection to image classification.  
  
We can also choose a custom model for advanced functions like Voice recognition, Smart prediction, etc, and then convert them to TFLite format. These can then be easily deployed in our Flutter app.  
  
Another handy resource is [Teachable Machines with Google](https://teachablemachine.withgoogle.com/train). This website allows even those with limited knowledge of AI/ML to create their own custom ML models.  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Using Teachable Machines with Google:**
-----------------------------------------

[Teachable Machines with Google](https://teachablemachine.withgoogle.com/train) is extremely useful for developers wanting to create and use an ML model quickly without any hassle. It offers options for Image Recognition models, Audio models, and Posture detection models. Let us see the process of creating an Image recognition model:  
  
First, we go to the website, click on Image Project, and click on Standard Image Model.  
  
Now we have our ML model training UI presented in front of us:  
  
![teachable_machines](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUk1pDgCdiSkUchqc0cbVsNI5QZwLW7C6xLX2LWS6KKn4zrcwFGbq2b_srA39p7xNK0RiMwN4tRzSNno01qPSBT1EAFCRCVFvNJOl7IgEkgTKm6H76IyBOMhWFzk_2WtjZ3QVz8iimkMQttnYjSr7_xjvNC0_SSs7rCtdlBY6tHWCe3Ox7eTQ2h6ZhIsM6/w320-h190/teachable_machines.png "teachable_machines")  
Here the different Classes represent the different categories our models should be able to classify into. Now we need to upload its training data set. Procuring training data is not that difficult of a feat. We can use available training datasets from sites like [Find Open Datasets and Machine Learning Projects | Kaggle](https://www.kaggle.com/datasets). If we want to create a custom dataset we can do that too. A simple way of achieving this is to run a Python script which will use Bing to make a query, and then download all the images that come up in response to that query. A great library for this is the [bing-image-downloader.](%22https://pypi.org/project/bing-image-downloader/%22)  
  
We can do this as follows:

```python
# Step 1: Install the required libraries
!pip install bing-image-downloader
# Step 2: Import the necessary modules and download images
from bing_image_downloader import downloader
# Define the keyword and number of images to download
keyword = "rural floods"
num_images = 100
# Download images to a directory in Colab
downloader.download(keyword, limit=num_images, output_dir='/content/rural_floods_images')
# Step 3: Move the downloaded images to local memory
import shutil
# Define the path to the downloaded images in Colab
colab_image_dir = '/content/rural_floods_images/' + keyword
# Define the path where you want to save the images locally
local_image_dir = '/content/'
# Move the images from Colab directory to local directory
shutil.make_archive(local_image_dir + keyword, 'zip', colab_image_dir)
# Verify that the images have been moved to your local directory
import os
local_image_zip = local_image_dir + keyword + '.zip'
if os.path.exists(local_image_zip):
    print(f"Images have been downloaded and saved to {local_image_zip}")
else:    
print("Image download failed.")
```

  
This gives us a rough dataset for our classes which we can then manually refine as per our needs. In our training UI, we create the different classes and click upload to set our dataset. After we are done with this, we can use the training window to set model parameters like Epochs, Batch Size, and Learning rate. Then we click on ‘train model’.  
  
After the model is done training, we can preview its results in the window itself as needed. Now we can change up the training parameters and re-train if desired or we can click ‘export’ to download our .tflite model.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**ML Model Deployment**
-----------------------

  
We first take our TFLite model and the labels.txt file and store them in our assets folder.  
Then, we add the TFLite dependency, and we run the pub get command:  
dependencies:  
flutter\_tflite: **^1.0.1**  
This gives us access to the TFLite package.  
Here, we will aim to deploy and run our model locally on our device. Now, we shall load the model locally.

```dart
void initState() {
 super.initState();
 loadModel();
}
loadModel() async {
 Tflite.loadModel(
     model: "assets/model_uquant.tflite",
     labels: "assets/labels.txt");
}
```

  
With our model loaded, we can use it however we wish. For example, if my model is an image recognition model:

```dart
detectImage(File img) async {
 var prediction = await Tflite.runModelOnImage(
     path: img.path,
     numResults: 2,
     threshold: 0.8,
     imageMean: 127.5,
     imageStd: 127.5);
 print(prediction);
}
```

  
This prediction gives us the output of the model based on the labels.txt file.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**ML Model Deployment using Interpreters**
------------------------------------------

Certain Custom models might not include a label.txt file but rather return a characteristic array for the image. For this, we must obtain the output using interpreters and then use some post-processing to obtain the output.  
Let's say our custom model is a resnet50 model that returns the characteristic array of the image provided.  
  
First, we install the tflite\_flutter package:  
dependencies:  
tflite\_flutter: **^0.10.4**  
The answer class will be predicted from labels.txt using the probability of indexes used in the Model.  
  
Now, our first task is to convert the image we have into a byte buffer so that our model can use it.  
  
We can do this as follows:

```dart
Future<List<List<List<List<double>>>>> getImageArray(File imageFile) async {
 img.Image? image = img.decodeImage(await imageFile.readAsBytes());
 // Resize the image to 224x224
 image = img.copyResize(image!, width: 224, height: 224);
 // Convert pixel values to floating point and normalize to range [0, 1]
 List<List<List<List<double>>>> imageArray = [];
 List<List<List<double>>> batch = [];
 for (int y = 0; y < image.height; y++) {
   List<List<double>> row = [];
   for (int x = 0; x < image.width; x++) {
     int pixel = image.getPixel(x, y);
     double red = (img.getRed(pixel)).toDouble();
     double green = (img.getGreen(pixel)).toDouble();
     double blue = (img.getBlue(pixel)).toDouble();
     row.add([red, green, blue]);
   }
   batch.add(row);
 }
 imageArray.add(batch);
 return imageArray;
}
```

  
Now we can use the package imported as tfl to obtain the characteristic array of our image.

```dart
Future<List<Map>> predictionList() async {
 final interpreter = await tfl.Interpreter.fromAsset(
     'assets/resnet50.tflite');
 List<List<List<List<double>>>> imageArray = await getImageArray(image); 
//get ImageArray converts the image file into a byteBuffer
 var input = imageArray;
 var output = List.filled(1 * 2048, 0).reshape([1, 2048]);
 interpreter.run(input, output);
 final outList = await getActualData(output[0]);
 return outList;}
```

  
**Post-Processing the data:**  
We can match the 1st array with all the arrays present in our JSON file(containing classes and respective characteristic arrays) and apply a KNN model to predict the name of the class to which the image resembles the most.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Conclusion**
--------------

This document outlines a general simple deployment of ML models. For more information and examples, visit the official pub.dev documentation at: [flutter\_tflite install | Flutter package (pub.dev)](https://pub.dev/packages/flutter_tflite/install) and [tflite\_flutter | Flutter package (pub.dev)](https://pub.dev/packages/tflite_flutter).
