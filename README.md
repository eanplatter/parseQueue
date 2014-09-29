#Introduction

Today we are going to be building a queue app similar to the one we use during class. Instead of a Firebase backend though, we will be using Parse. 

Sign up for an account at Parse: http://parse.com

Then once logged into Parse, create a new app. After the app is created you will be shown your API keys. Don't leave this page until you have set up your keys. 

Throughout this project, don't hesitate to check out the Parse API documentation. Being able to get answers from someone's documentation is an important skill. 

View it here: https://parse.com/docs/rest

To do that create a file in your js folder called 'defaultHeaders.js'. Then copy your Application id and REST API key into the following code:

````javascript
	var app = angular.module('parseQ');

	app.factory('httpRequestInterceptor', function () {
	  return {
	    request: function (config) {
	      config.headers = {'X-Parse-Application-Id': 'INSERT-YOUR-APPLICATION-ID', 'X-Parse-REST-API-Key': 'INSERT-YOUR-REST-API-KEY'}
	      return config;
	    }
	  };
	});
````


Parse is good because it encourages us to create a RESTful API. We will learn how to make the 4 HTTP requests with AgularJS:

<ul>
	<li>GET - retrieve data</li>
	<li>POST - create data</li>
	<li>PUT - edit data</li>
	<li>DELETE - delete data</li>
</ul>

#Step 1 - Set Up Application

The first thing we need to do is create and link all of our files. ** The AngularJS CDN is already loaded into the app, no need to look for outside code. **

<ul>
	<li>Create MainController.js in the *controllers* folder and link it in the index</li>
	<li>Create parseService.js in the *services* folder and link it in the index</li>
	<li>Link the main.css file in the index</li>
	<li>Link the app.js file in the index</li>
</ul>

We next want to ensure angular is working correctly, first connect your view and controller: 

<ul>
	<li>Create your angular module and palce it in all of your JavaScript files. *remember: var app = angular.module('parseQ', [])*</li>
	<li>Place the ng-app into your index</li>
	<li>Create your MainController and place it in your index using ng-controller</li>
</ul>

Then, create a test:

<ul>
	<li>In your MainController create a $scope.test object and give it a value</li>
	<li>Call the $scope.test object in view to ensure it's pulling the value from the controller.</li>
</ul>

#Step 2 - Creating Questions

We will begin by making it possible to create questions, primarily because this is the most important feature of our queue. 

Let's start with our service as it will be where our data begins and ends. 

<ul>
	<li>Go to your parse service and create a POST method, that takes in a question as a parameter. *Don't hesitate to refer to the chat app we made last week.*</li>
</ul>

##SIDENOTE

As a reminder, here is the anatomy of a POST GET PUT and DELETE request in AngularJS:

###POST: https://parse.com/docs/js_guide#objects-saving

<ul>
	<li>A Deferred variable for your promises</li>
	<li>An $http request:</li>
	<ul>
		<li>The *method* of the request</li>		
		<li>The data object you're passing in</li>
		<li>the URL of the reqest</li>
	</ul>
	<li>An appended promise object</li>
	<li>lastly return the promise object</li>
</ul>

###GET: https://parse.com/docs/js_guide#objects-retrieving

<ul>
	<li>A Deferred variable for your promises</li>
	<li>An $http request:</li>
	<ul>
		<li>The *method* of the request</li>		
		<li>the URL of the reqest</li>
	</ul>
	<li>An appended promise object</li>
	<li>lastly return the promise object</li>
</ul>

###PUT: 

<ul>
	<li>A Deferred variable for your promises</li>
	<li>An $http request:</li>
	<ul>
		<li>The *method* of the request</li>		
		<li>The data object you're editing</li>
		<li>the URL of the reqest</li>
	</ul>
	<li>An appended promise object</li>
	<li>lastly return the promise object</li>
</ul>

###DELETE:

<ul>
	<li>A Deferred variable for your promises</li>
	<li>An $http request:</li>
	<ul>
		<li>The *method* of the request</li>		
		<li>The data object you're deleting</li>
		<li>the URL of the reqest</li>
	</ul>
	<li>An appended promise object</li>
	<li>lastly return the promise object</li>
</ul>

<hr>

After creating our POST request, we need to head over to the controller so that our users can create data on their own from the view. 

In the controller create a postData function. This function will take in our question from the view and pass it into the service. Refer to the chat app, it will have a very similar function.

Now that our service is opening a connection from our app to Parse, and our controller is ready to take data in from the view and pass it to the service, we need to get our view set up!











