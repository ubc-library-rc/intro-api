---
 layout: default
 title: What is an API?
 parent: Outline
 nav_order: 1
---
# What is an API?

<em><a href="../slides/what-is-an-api.html" target="_blank">View slides</a> for this section</em>

**API** stands for "Application Programming Interface". In the simplest terms an API is just a structured way for software applications to communicate with each other.

An API can give you access to the services or data available from another software application. When the application receives a specially formatted request -  referred to as an API _call_ - it responds by providing the requested service or data in a way that can be integrated into other applications or workflows.

## Why use APIs?
APIs are often used by software developers to enhance their own projects. Instead of building everything from scratch developers can use APIs to take advantage of services offered by other applications. For example, the Google Maps API makes it relatively easy to incorporate an interactive map into your project - there's no need to create your own.

#### Example: Google Map API
<iframe width="400" height="300" frameborder="0" style="border:0"
src="https://www.google.com/maps/embed/v1/view?zoom=11&center=49.2827,-123.1207&key=AIzaSyDYl5y6Sq0XKodDmTDWuKV1VYMLcMmT_QM" allowfullscreen></iframe>
Source: <a href="https://developers.google.com/maps/documentation/embed/start" target="_blank">Google Maps Embed API</a>_

You don't need to be a developer to benefit from APIs: They're also useful for extracting data from web services in a structured format. Take Google Analytics as an example. The Google Analytics website provides several dashboards designed to answer the most common questions about website activity. This is often helpful, but it can be frustrating when you need the data packaged differently than the website allows for. That's where an API can help: using the Google Analytics API you can request the underlying data in a flexible format - usually JSON or XML - then use your own tools to explore or package it the way you need to.

For the service provider, APIs provide a way to control and monitor access to their resources

##  The restaurant metaphor: API as waiter

Some people find it helpful to think of an API as a waiter taking and delivering orders in a restaurant. Andrew Park describes this metaphor [in his blog](https://tray.io/blog/how-do-apis-work):

> _Imagine you’re a customer at a restaurant. The waiter (the API) functions as an intermediary between customers like you (the user) and the kitchen (web server). You tell the waiter your order (API call), and the waiter requests it from the kitchen. Finally, the waiter will provide you with what you ordered._

> _As a customer, you don’t need to know how the kitchen or the restaurant operates in order to get what you want: the food. You just need to know how to order it._

That last sentence - *you just need to know how to order it* - is important to remember. Though APIs for different services have a common structure, each will have its own options. You will need to read a particular API's documentation to understand what is available and get results.

## RESTful APIs
There are many kinds of APIs. In this workshop we focus on RESTful APIs, where the communication between applications happens via HTTP and often using a browser.

**REST** stands for "Representational State Transfer," referring to an architecture common in web APIs. In RESTful APIs, calls are sent through a browser and the details of each request are embedded in the URL.
{: .note}

The REST architecture expects there to be a __server__ and a __client__. The server is where the data lives and the client is what makes the API call to the server. Communication can go both ways but generally writing data to a server is more restricted than getting data from a server.

## Authentication and API keys
Generally an API is doing two things:
* supporting communication between tools
* controlling access to resources

The way APIs control access to resources is through __authentication__ (identifying who you are) and __authorization__ (determining what you're allowed to access). You're already familiar with a common form of authentication, the username and password. Another form of authentication used with APIs is the **API key**. An API key is an identifier embedded in your API calls that identifies you and determines what you're authorized to access from the server.

There are different types of API keys. A **public** API key is one that anyone can use without additional identification. Public keys often provide limited access to the server's resources. A public key might let you get a _list_ of what is on a server, for example, but to access the full contents you may need to provide more information about your identity and get a **registered** API key. The type of key usually determines the number of calls you can make within a certain amount of time, to avoid overloading the server or blocking others from accessing it.
