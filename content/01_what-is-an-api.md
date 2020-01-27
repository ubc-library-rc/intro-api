---
 layout: default
 title: What is an API?
 parent: Outline
 nav_order: 1
---
# What is an API?

**API** stands for "Application Programming Interface". In the simplest terms an API is just a structured way for software applications to communicate with each other. An API provides access to certain services or data. When the application receives a specially formatted request - also referred to as an API _call_ - it responds by providing the requested service or data in a way that can be integrated into other applications or workflows.

There are many kinds of APIs. In this workshop we will focus on web APIs, where the communication between applications happens via HTTP. In this type of API the calls are sent through a regular web browser and the details of each request are embedded in the URL.

You may come across references to RESTful APIs. REST stands for "Representational State Transfer" and refers to a type of API architecture that is common in open web APIs like the ones introduced in this workshop.
{: .note}

## Why use APIs?

APIs are often used by software developers to incorporate data or services into their own projects. Instead of building everything from scratch, developers use APIs to take advantage of services offered by other applications or platforms. For example, the Google Maps API makes it relatively easy to incorporate a custom map into your project - there's no need to draw a map from scratch.

But you don't need to be a developer to benefit from APIs. They're also useful for extracting data from applications or web services in a more flexible format. Take Google Analytics as an example. The Google Analytics website provides several dashboards designed to answer the most common questions about website activity. This is often helpful, but it can be frustrating when you need the information packaged differently than the website allows for. That's where an API can often help: using the Google Analytics API you can request the underlying raw data in a flexible format - usually JSON or XML - then use your own tools to explore or package it the way you need.

##  The restaurant metaphor: API as waiter

Some people find it helpful to think of an API as a waiter taking and delivering orders in a restaurant. Andrew Park describes this metaphor [in his blog](https://tray.io/blog/how-do-apis-work):

> Imagine you’re a customer at a restaurant. The waiter (the API) functions as an intermediary between customers like you (the user) and the kitchen (web server). You tell the waiter your order (API call), and the waiter requests it from the kitchen. Finally, the waiter will provide you with what you ordered.

> As a customer, you don’t need to know how the kitchen or the restaurant operates in order to get what you want: the food. You just need to know how to order it.
