---
 layout: default
 title: Working with APIs
 nav_order: 5
---

## Structure of a Query

<em><a href="../slides/working-with-apis.html" target="_blank">View slides</a> for this section</em>

A query has a few core components:
* __endpoint__
* __path__
* __query parameters__

Every API has an __endpoint__ which is like providing an address to the server. This is the first piece of information REST expects you to have. For example, if you wanted to get data from the Numbers API (which serves trivia about numbers) through an API call, the endpoint would be: http://numbersapi.com.

The __path__ tells the server which data you are most interested in and __query parameters__ are a way to further specify what you want. Query parameters are not a part of the REST architecture but are commonly used.

A query doesn't have to lead to only one thing. It's also possible to batch your requests by indicating that you are interested in more than one piece of data. For the Numbers API this means you might be interested in facts about multiple numbers.

This is just the tip of the iceberg! A lot more is possible with APIs and we will touch on next steps through our activities.

## Case study: Querying The Cat API

[TheCatAPI](https://thecatapi.com) is a free web API with information about cat breeds and a database of cat images. The API can be used to search the database, display cat images, upload new images, and tag your favorites. In this activity we'll use the API to return information about and display a series of cat images.

### The basics: one random cat
Open a new browser tab or window. Copy the URL below into the address bar and hit _enter_.

Input
{: .label .label-green }
```
https://api.thecatapi.com/v1/images/search
```

The API call returns a JSON string with information about one random entry in the cat image database. For example:

Output
{: .label .label-yellow }
```
[{"breeds":[],"id":"MTk1ODY2Mw","url":"https://cdn2.thecatapi.com/images/MTk1ODY2Mw.jpg","width":640,"height":480}]
```

To view the image, copy the URL portion of the JSON string into the address bar, then hit _enter_.

### Getting specific: query parameters
That's quite a bit of work for one random cat image but we can refine results with query parameters. Add a `?` to the end of the URL followed by one or more parameters in the format shown below. Note that each parameter is separated by a `&`.

Input
{: .label .label-green }
```
https://api.thecatapi.com/v1/images/search?breed_ids=rblu&limit=5
```

This will return a JSON string with information about five (limit=5) images of Russian Blue cats (breed_id=rblu).

Input
{: .label .label-green }
```
https://api.thecatapi.com/v1/images/search?category_ids=5&format=src
```

This example returns an image instead of a JSON string (format=src) showing a cat in the "boxes" category (category_ids=5).

### Mix and match
The [API documentation](https://docs.thecatapi.com/) lists the available query parameters and their acceptable values. Below are some examples you can experiment with.

#### *category_ids* parameter

| category | parameter value
| --- | ---
| boxes | 5
| caturday | 6
| clothes | 15
| funny | 3
| hats | 1
| kittens | 10

#### *mime_types* parameter
Limits output to specified file type: jpg, png, or gif.

#### *format* parameter
Default output format is JSON, but setting this parameter to `src` displays the image itself.
