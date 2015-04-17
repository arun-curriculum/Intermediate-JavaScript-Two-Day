#Intermediate JavaScript Continued

##AJAX
- AJAX is a powerful way to create server requests and get responses without having to reload the page.
- AJAX stands for Asynchronous JavaScript and XML.
- Here is how it can be accomplished:

```
function reqListener () {
	console.log(this.responseText);
}

var oReq = new XMLHttpRequest();
oReq.onload = reqListener;
oReq.open("get", "[Endpoint Here]", true);
oReq.send();
```

- XMLHttpRequest is an object that contains the methods to send AJAX requests.
- The most important method here is `.open`, which takes three parameters:
	- Type of request
	- URL endpoint
	- Asynchronous true or false
- `.send` submits the request.

##AJAX Exercise
- Let's make a request out to `http://daretodiscover.herokuapp.com/users`.
- We can evaluate how we can get data into the console about each user.

##In-Class Lab
- Make a GET request call out to `http://daretodiscover.herokuapp.com/wines`.
- Take the returned data and create a simple HTML template to show the data for each wine.

####How to Use Handlebars
- Handlebars templates are handled through `<script>` tags, which allow them to be ignored while rendering the page:

```
<script id="my-template" type="text/x-handlebars-template">
```

- You can write any normal HTML here, but you can also write Handlebars-specific code:

```
<script id="my-template" type="text/x-handlebars-template">
	<div class="entry">
		<h1>{{title}}</h1>
		<div class="body">
			{{body}}
		</div>
	</div>
</script>
```

- The curly code is essentially keys to a JSON object.
- If you need to, you can also loop through an array of JSON objects to produce very dynamic templates. You will do this today. Here is an example from the docs on how this can be done through helpers:

```
<h1>Comments</h1>

<div id="comments">
	{{#each comments}}
		<h2><a href="/posts/{{id}}">{{title}}</a></h2>
		<div>{{body}}</div>
	{{/each}}
</div>
```

- This example assumes that `comments` is an array of JSON objects.

- Before a template is used however, it must be first "compiled":

```
var source = document.getElementById("my-template").innerHTML;
var template = Handlebars.compile(source);
```

- The function `Handlebars.compile` returns a function that can be passed JSON data as an argument.
- This resulting function returns HTML after the JSON data is processed into it.
- You can then apply your template anywhere you need to:

```
var jsonData = {
	title: "My New Post",
	body: "This is my first post!"
};

var template_html = template(jsonData);
document.getElementById("some-div").innerHTML = template_html;
```

##Book List with Handlebars
- We will be creating a simple book list system using handlebars to take care of the templating.
- The API for this exercise will be `http://daretodiscover.herokuapp.com/books`.
- The HTML is already done for you [here](book_manager_html/).

##Querying Real-Life APIs
- API stands for Application Programmable Interface. It essentially gives you access to a limited set of the application's features in a structured and controlled way.
- APIs vary in their implementations. There is usually no one-way to query all of them.
- There are a few popular APIs that many developers implement:
	- Facebook: Get user information and post statuses.
	- Twitter: Get user information and post tweets.
	- Google Maps: Render maps based on location data with custom markers.
	- Meetup: Get location-based event information.

##Query Structure
- Many times the query will exist in the URL of the request.
- Let's take a look at a popular API for getting information about movies: [http://www.omdbapi.com/](http://www.omdbapi.com/).
- Queries can be made by adding to the URL:

General Search

```
http://www.omdbapi.com/?s=The+Avengers
```

Pull by title

```
http://www.omdbapi.com/?t=The+Avengers
```

##Formatting Data
- In order to use data entered by a user for the query it is important to format it appropriately for use in a URL.
- JavaScript has a built-in method to do this:

```
var query = document.getElementById("query").value;

encodeURIComponent(query);
```

##API Exercise: Getting Movie Information
- OMDb is an open API that gives us access to movie information.
- Let's check out the documentation [here](http://www.omdbapi.com/).
- Check out how you can make queries to the API using query string parameters (?t=My+Title).
- Here are the steps you will need to take:
	- Step 1: Grab the information that the user enters into the form.
	- Step 2: Query the API using the entered title and display the JSON results in the console.
	- Step 3: Take the JSON and create a Handlebars template to show the information. The HTML has already been completed for you [here](movie_starter_app/).