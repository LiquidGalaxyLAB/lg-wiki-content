---
title: How to build a back-end using Flask to integrate your app with machine learning features?
contributor: Peter Atef
date: 2024-06-12T13:06:24.805+00:00
---

  
_**Pre-knowledge**_  
  
Before we start talking about Flask, there are a few things we need to do  
1 - Create a Python environment. 2 - Install the following libraries: a - flask  
b - python-dotenv  
c - requests  
→ I recommend using anaconda for step #1 and you can get all the steps needed to create a conda environment from the documentation [link](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)  
→ For step #2, you can name the file requirements.txt, and add the following text:  
Then run on of those commands:  
pip: pip install -r requirements.txt  
Conda: conda install --yes --file requirements.txt  
  
![instalin conda](https://lh7-us.googleusercontent.com/docsz/AD_4nXeAHpBV6sAWUo4ZKuwTTnxFhPneYIzdVXEw9mH3F0P8i0mEFcOyMNDCWEKMKEkWRqtuhmgX1RaMpzmQQqth42kERExMcWkVWiWPDqE0pWKVSmSc-R-Df8TrKcvU1roTHQFG_u4pZq9i-JnFsDmvyES3puwO?key=eXYxpY5rbSPIPtG3SWVZIQ "instalin conda")  

* * *

  
_**Introduction**_  
  
## Flask fundamentals
Flask is an open-source web "micro-framework". When the creators use the term "micro-framework", they mean that the framework will perform the required tasks of a web framework, but that it doesn't include advanced features, or other specific requirements that your application must follow to work correctly. This approach allows Flask to be extremely flexible, and perfect for use as a front end to existing back ends or APIs - like Azure AI services!  
  
When creating a web application with any framework, there are a couple of core concepts we need to understand - routing, methods, and templating. Let's explore these concepts before we write our code.  
  
## Responding to user requests with routes
  
When a user uses a web application, they indicate what they want to do, or the information they're seeking, by browsing to different uniform resource locators (or URLs). They might type out an address directly (say https://adventure-works.com), or select a link, or a button that includes the appropriate URL. On an e-commerce site, you might have URLs that look like the following:  
  
→ https://adventure-works.com/ for the main page  
→ https://adventure-works.com/products/widget for details on a Widget  
→ https://adventure-works.com/cart/buy to complete a purchase  
  
As a developer, we don't need to worry about the first part of the URL, or the domain (adventure-works.com in our example). Our application is put into action based on whatever comes after the domain name, starting with the /. The portion after the domain name is what's known as a route.  
  
A route is a path to an action. Similar to tapping on a button in a mobile app, a route indicates the action the user wants to perform. We'll register different routes in our web application to respond to the various requests our application supports.  
In our application, we indicate how we want to respond to a particular route request by providing a function. A route is a map of a function. When we think about writing code in general, this concept is relatively natural. When we want to perform a particular action, we call it a function. Our users will do the same thing! They'll just do it a little differently, by accessing a route.  
  
## Methods or verbs
  
→ Routes can be accessed in many ways, through what are known as methods or verbs (the two terms mean the same thing and can be used interchangeably). How the route is accessed provides additional context about the state of the user request and what action the user wants to perform.  
→ There are many methods available when creating a web application, but the two most common (and the only two we'll focus on) are GET and POST. GET typically indicates that the user is requesting information, while POST indicates that the user needs to send us something and receive a response.  
  
A common application flow that uses GET and POST revolves around using a form. Let's say we create an application where the user wants to register for a mailing list:  
1 - The user accesses the sign-up form via GET  
2 - The user completes the form and selects the submit button  
3 - The information from the form is sent back to the server by using POST  
4 - A "success" message is returned to the user  
  
As you might suspect, the user doesn't directly indicate the verb they want to use, it is controlled by the application. Generally speaking, if the user navigates to a URL directly, by typing it in or by selecting a link, they access the page by using GET. When they select a button for a form, they typically send the information via POST.  
  
## Templates
  
Hypertext Markup Language, or HTML, is the language used to structure the information displayed on a browser, while Cascading Style Sheets, or CSS, is used to manage the style and layout. When creating an application, most of the HTML will be static, meaning it won't change. However, to make our pages dynamic we need to be able to programmatically put information into an HTML page. Nearly every web framework supports this requirement through templates.  
  

* * *

  
_**References**_  
  
1 - [Microsoft documentation](https://learn.microsoft.com/en-us/training/modules/python-flask-build-ai-web-app/0-introduction)  
2 - [Build an AI web app to translate text using Python Flask](https://youtu.be/EKXSqvdlOIg)
