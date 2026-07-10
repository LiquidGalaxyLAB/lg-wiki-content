---
title: How to add beautiful animations using Lottie/Hero?
contributor: Saumya Bhattacharya
date: 2024-06-07T08:27:19.163+00:00
---
## Overview
Let’s first understand what Lottie is.  
Lottie is a library developed by Airbnb that allows us to render animations and vector graphics in real-time. Lottie enables developers to include complex animations in their applications with minimal performance impact.  
  
Here's a brief explanation of how Lottie is used in Flutter:  
  
_**1 - Installation:**_ we need to add the lottie package to your Flutter project's pubspec.yaml file.  
  
![dependency](https://lh7-us.googleusercontent.com/docsz/AD_4nXcJRgo2w81cebiPEpe9XMuFlUg11bZNqdvbvN-Rc23OIFNZTUvA4sXEfwfNbZLHly6rfbKgHrA3Nyl369WTMg2qV2r6n6sgSCgOcBjJhumLTroz7lgW8RM9j3tVt6IaRdCHBqCLAlVdiuPeAi_kmFnAUyY?key=tUpKevYTxy98FMSNVHBroQ "dependency")  
_**2 - Import:**_ Import the Lottie package in your Dart file where we want to use the animation.  
  
![package](https://lh7-us.googleusercontent.com/docsz/AD_4nXdTD10JpBEt6S7LJmccx2aTmj_pvFtnhXwr2U2WK_TGpKSmZN69aLT2qzLXQUswW416X-XRCjTN0PS569mD4-SqVHcxtO70CAagUk9SS4ZvMzmppcCCwfXBWLbyt3hZR0QRH9M1Y2SjqGAvKA6hSnuLJeiz?key=tUpKevYTxy98FMSNVHBroQ "package")  
_**3 - Usage:**_ we can load and display Lottie animations using the Lottie.asset() or Lottie.network() constructor. For example, if we have an animation file named animation.json in your assets folder:  
  
![asset](https://lh7-us.googleusercontent.com/docsz/AD_4nXf_gBon4h5v_LJlxvpMmPDtlX6x71p2Pmz9NC1SIjvGXgkfvHKQHHhEEIWlpdLUylvBRo--M976CrJuSvnHmji4UXXlmgw2lHhARQaRkVxD6OPr9racUmik95LMv_RkdFlQegsuYP7I9HZ0LdLL9WYOZPE?key=tUpKevYTxy98FMSNVHBroQ "asset")  
Here's a simple code example demonstrating the usage of Lottie in Flutter:  
  
In the below example, the Lottie.asset() widget loads and displays an animation stored in the assets/animation.json file.  
  
![lottie](https://lh7-us.googleusercontent.com/docsz/AD_4nXfPJmT_QsLha8t6ilxyJssttkz5gOPZnk3W2LtqygLD1UukQ3YmalTXFZKfK-Dn5GG9dW5zLqjjaUVPN-qUnDifx18RBCHUMZjIIhAthxa0wU4SSlJn9plPDstLLxFzpVqLJJi8Dpp5vYyqUJ3dFNo8cIAJ?key=tUpKevYTxy98FMSNVHBroQ "lottie")  
That's all, I hope this helps. Happy Coding!
