---
 layout: default
 title: Working with APIs
 parent: Outline
 nav_order: 3
---
# Working with RESTful APIs

The REST architecture expects there to be a "__server__" and a "__client__". The server is where the data lives and the client is what makes the API call to the server. Communication can go both ways but generally writing data to a server is more restricted than getting data from a server.

Generally an API is doing two things:
* supporting communication between tools
* controlling access to resources

The way that access to resources is limited on the web is through authentication (where a tool wants to know who you are) and authorization (where a tool lets you do a certain thing). A common form of authentication that you are familiar with is username and password. Something you will run into when working with APIs is the concept of an "API key". An API key is like an identifier for your client that identifies you and, based on the type of key, authorizes you to do certain things. For example a "Public" API Key (one anyone can use without additional identification) might let you get a list of what is on a server but a "Registered" API Key (one where you had to provide more information about your identity) might let you get the full contents of what is on the server. The type of authorization you receive usually restricts the number of calls you can make within a certain amount of time to avoid overloading the server or blocking others from accessing it.

## Structure of a Query

A query has a few core components:
* __endpoint__
* __path__
* __query parameters__

Every API has an __endpoint__ which is like providing an address to the server. This is the first piece of information REST expects you to have. For example, if you wanted to get data from the Numbers API (which serves trivia about numbers) through an API call, the endpoint would be: http://numbersapi.com.

The __path__ tells the server which data you are most interested in and __query parameters__ are a way to further specify what you want. Query parameters are not a part of the REST architecture but are commonly used.

For example, in the Numbers API a path could be:
~~~
http://numbersapi.com/random/year?
~~~
which indicates that you would like the API to give you a _random_ trivia fact about a number from any _year_.

If you were more discerning and wanted to only hear trivia from the year 1950, the path would look like this:
~~~
http://numbersapi.com/1950/year?
~~~
<details>
<summary>Try entering http://numbersapi.com/1950/year? into a browser search bar. What output did you get?</summary>
<br>

Output
{: .label .label-yellow }
~~~
1950 is the year that nothing remarkable happened.  
(Or some equally pithy comment.)
~~~

</details>

If you want to further specify what you want to get out of the API, __Query parameters__ are added on using this structure:

~~~
?query1=value1&query2=value2
~~~

The symbol "?" indicates the end of the path and the beginning of the __query parameters__.

For example, if we want to always get the same comment when we search a year in which nothing happened we can specify that by providing our own default parameter.
~~~
http://numbersapi.com/1950/year?default=Nothing+happened.
~~~

A path doesn't have to lead to only one thing. It's also possible to batch your requests by indicating that you are interested in more than one path. For the Numbers API this means you might be interested in facts about multiple numbers.

For example, if you were interested in facts about all of the numbers from 1 - 100 you could write:
~~~
http://numbersapi.com/1..100
~~~

Or if you wanted to get facts about 100, 200, and 300 but skip everything in between you could write:
~~~
http://numbersapi.com/100,200,300
~~~

This is just the tip of the iceberg! A lot more is possible with APIs and we will touch on next steps through our activities.
