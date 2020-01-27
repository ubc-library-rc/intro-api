---
 layout: default
 title: Activities
 parent: Outline
 nav_order: 4
---
# Activities

## 1. Querying The Cat API
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


## 2. Querying the Open Collections API
The UBC Library's [Open Collections](https://open.library.ubc.ca/) has a robust open API which anyone can use though you do need to register an email address in order to make large or more involved requests.

Detailed documentation about the API is [available here](https://open.library.ubc.ca/docs).

### 2.1 Through OpenRefine
A quick and easy way to get data from an API endpoint is through the "Web Addresses (URLs)" function in OpenRefine. All you need to make use of this is a well structured query with the parameters that you want to get.

We will be using a common example in the UBC Library Open Collections documentation: [https://oc2-index.library.ubc.ca/collections/arkley/items](https://oc2-index.library.ubc.ca/collections/arkley/items). This query returns a list of all of the items in the Arkley Croquet collection.

1. First try pasting the query into a browser window to see whether any errors come up. This is a quick and easy way to check that your query is well structured.

2. Open OpenRefine and paste your query string into the "Web Addresses (URLs)" option under "Get data from".
![Paste query into OpenRefine](openrefine-weburl-paste-query.png)

3. OpenRefine will ask you to identify what you want out of the data.
![Identify data](openrefine-weburl-id-data.png)

After doing this you should see a preview that is a bit more readable.
![Identify data](openrefine-weburl-preview.png)

4. Select "Create Project" which processes the rest of the data and transforms the JSON into a tabular format. To view more records select "show 50" and you will end up with something like this:  
![Identify data](oopenrefine-weburl-output.png)

From here you can keep working in OpenRefine or export the data.

### 2.2 Through a Python script

For this activity we will be working in [UBC Syzygy](https://ubc.syzygy.ca/). Syzygy is a collection of research tools that are accessible through a web browser. One of these tools is "Jupyter" which is an electronic notebook that lets you run scripts in common programming languages and see the output immediately with no additional installation or setup required.

We are also going to follow the instructions in the [Open Collections documentation](https://github.com/ubc-library/docs-open-collections-api/blob/master/scripts/all_items_from_a_collection/all_items_from_a_collection.py). You do not need to read the full documentation to complete this activity but we encourage you to explore it if you are interested in learning more about what's possible with the Open Collections API.

1. Please log in to [UBC Syzygy here](https://ubc.syzygy.ca/). Click on the red house and log in via UBC CWL.
![Log in to Syzygy](syzygy-login.png)
2. In the upper right hand side of the page select "New" and then "Python 3" from the dropdown.
![Select Python 3 for new Jupyter notebook](jupyter-python3-select.png)
3. The Open Collections documentation has several open scripts for you to experiment with. We will be using the Python version of the script that retrieves a list of all of the items in a collection and their metadata (descriptive information about them). You can take a look at this script in [Github here](https://github.com/ubc-library/docs-open-collections-api/blob/master/scripts/all_items_from_a_collection/all_items_from_a_collection.py).

<details>
<summary>This script was originally written by Sean McNamara @Seanmcn for the UBC Library.</summary>
<br>
~~~ python
import requests, math, json

ocApiUrl = 'https://oc-index.library.ubc.ca'
apiKey = 'ac40e6c2cb345593ed1691e0a8b601bba398e42d85f81f893c5ab709cec63c6c'
collection = 'darwin'
perPage = 25
offset = 0

# Query the API for the collection item count
collectionUrl = ocApiUrl + '/collections/' + collection + '?api_key=' + apiKey
apiResponse = requests.get(collectionUrl).json()
itemCount = float(apiResponse['data']['items'])

# Figure out how many pages there are
pages = int(math.ceil(itemCount / float(perPage)))

# Loop through collection item pages to get all items
itemIds = []
for x in range(0, pages):
    collectionItemsUrl = ocApiUrl + '/collections/' + collection
    collectionItemsUrl += '/items?limit=' + str(perPage) + '&offset=' + str(offset) + '&api_key=' + apiKey
    offset += 25
    # Get list of 25 items
    apiResponse = requests.get(collectionItemsUrl).json()
    collectionItems = apiResponse['data']
    # Add each item id to the itemIds list
    for collectionItem in collectionItems:
        itemIds.append(collectionItem['_id'])

# Store all the items so we can print them out later
items = []
for itemId in itemIds:
    itemUrl = ocApiUrl + '/collections/' + collection + '/items/' + itemId
    apiResponse = requests.get(itemUrl).json()
    item = apiResponse['data']
    items.append(item)

print(json.dumps(items))
~~~

</details>
4. Copy the script as it currently is and paste it into the dialog box in your new Jupyter notebook,
![Paste script into Jupyter](paste-into-jupyter.png)
and run the script.
![Run in Jupyter](run-jupyter.png)

5. After a few moments you will see the output of your API call in the Jupyter notebook. At this stage your output is in JSON format.
![Jupyter output](output-in-jupyter.png). As a final step, let's turn this into tabular data through Open Refine.

6. Select all of our JSON output in the Jupyter notebook. A quick way to do this for a small amount of data is to select the beginning of our output, hold "Shift" and then select the end. CMD+C or CTRL+C to copy. Open OpenRefine and paste your copied output into the OpenRefine "clipboard" input.
![Paste into OpenRefine](paste-into-openrefine.png)

After selecting "Next" OpenRefine will ask you to explain the data to it a bit. For this exercise you need to tell it where the data begins that you want to see in a tabular format.
![Identify data](openrefine-id-data.png)

From here you can keep working with the data in OpenRefine or you can export it into a more familiar format to work with in another tool such as Excel.
!(Export data](export-to-csv.png)
