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

The first thing we need to do is create and link all of our files. The AngularJS CDN is already loaded into the app, no need to look for outside code.

<ul>
	<li>Create MainController.js in the controllers folder and link it in the index</li>
	<li>Create parseService.js in the *services* folder and link it in the index</li>
	<li>Link the main.css file in the index</li>
	<li>Link the app.js file in the index</li>
</ul>

We next want to ensure angular is working correctly, first connect your view and controller: 

<ul>
	<li>Create your angular module and palce it in all of your JavaScript files. remember: var app = angular.module('parseQ', [])</li>
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

###POST: https://parse.com/docs/rest#objects-creating

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

###GET: https://parse.com/docs/rest#objects-retrieving

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

###PUT: https://parse.com/docs/rest#objects-updating

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

###DELETE: https://parse.com/docs/rest#objects-deleting

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

In the index file we need: 

<ul>
	<li>An input field that takes in the actual question (ng-model)</li>
	<li>A button that submits our question into postData function in our controller (ng-click) </li>
</ul>

Once everything is in place, we should be able to ask a question from our browser and then see that question in our Parse dashboard. 

#Step 3 - Retrieving Questions

Once we are able to save our questions to our Parse database we will want to retrieve those questions so that we can see them in our view! 

Let's start:

<ul>
	<li>Create a getData function in your service</li>
	<li>Then create a getParseData function in your controller, which will import the getData function from your service</li>
</ul>

The getParseData will be an important function through our app. We will need to call it everytime we do anything else. This ensures that everytime our app changes we see those changes. 

Add the getParseData function to our postData function within our controller, so that as we add a new question it calls the data.

Now at the bottom of our getParseData function let's add a console.log that will show us the data it retrieves. 

If we enter a question we should see an array of objects in our console. 

Now you can show your in your view:

<ul>
	<li>ng-repeat through the array showing the 'text' of each question</li>
	<li>Make sure that now when you add a new question it shows up instantly in the list of questions.</li>
</ul>

If everything is working it's time to move into editing our questions!

#Step 4 - Editing Questions

Once we have a list of students asking questions in the queue, we need to be able to escalate those questions to show which ones are being handled. 

We should have created our postData function in our service that takes in a question. In the data section of that $http request, we said: data: {text: question}. Now we want to add another key-value pair to the questions so that they have not only a text attribute, but also a status attribute. 

Let's do that by just creating a default status of 'red'. We will say new questions have the status of 'red', while questions that are 'being helped' will have a status of 'yellow'. 

This will make it easy for our filters to know where to show new and old questions.

Now that each question will have a default status of 'red', we need to make a way to change that status. 

<ul>
	<li>Create a updateData function in our service. It will be similar to the postData however this time we will be using 'PUT' </li>
	<li>To updated an object you will need to target it by the objects Id, passing it in as a url parameter.</li>
	<li>Create a changeStatus function in the controller that takes in the updateData function from the service. </li>
	<li>In your index create a button within your ng-repeat that runs the changeStatus function. This button should change the questions status from 'red' to 'yellow'</li>
	<li>Add a filter to the original ng-repeat so that it only shows objects with the status of red</li>
	<li>Create a new ng-repeat that filters out only the objects with the status of yellow</li>
</ul>

Now we should be able to create a new question, watch it show up in the new question list, then move it to the 'being helped' or yellow list.

#Step 5 - Delete Questions

Once we have answered someones question, we want to remove it from the list. We could easily do this by changing the status from yellow to something other than red and yellow. Then it wouldn't show up on any of the ng-repeats, but instead we are actually going to delete our questions from Parse. 

<ul>
	<li>Create a function on our service called deteleData. This function is similar to our get data function, but it targets a single object via it's objectID and uses the delete method.</li>
	<li>Then create a function in the controller that pulls the detele function from the service.</li>
	<li>Then in the ng-repeat that shows yellow questions create a button that calls the delete function from the controller.</li>
</ul>

Now we should be able to delete our questions once they have been answered! 

Wowee!















