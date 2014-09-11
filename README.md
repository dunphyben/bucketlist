Coders Workshop Day 2

Agenda:

UI Walkthrough
Add data to the backend
Retrieve data using app services
Whta if you have no connection?
Add a new item from the app
Geolocation
Users, groups and roles
Creating, updating and deleting connections
Run on mobile

j.mp/a-filename-here

j.mp/apigee-learn-app

Install for android
	j.mp/apigee-pg-install


Mobile apps can be used offline
	Main differentiator between app and website

### Ways to build mobile apps
	* Native
		* Pro:
			* Have full access to all underlying architechture of the device. Implies that performance is going to be better. But that is a lie. You will get gains only for gaming, 3-d games etc.
		* Cons:
			* Cross-platform problems. 
				* The apps will start to grow apart
				* Certain features on Android won't translate on iOS, vice versa etc.
			* You have to have talent in Java, C#, Obj-C

	* PhoneGap
		* html css and js
		* can use angular, ember, or any other js library or framework
		* Phonegap is a wrapper
			* Provides hooks via javascript to all the underlying archicture of the device your running on
				* Makes it essentially native
		* Very few things you can't get to with phonegap that you can do with native pps
			* 3-d gaming is the only thing that you can't use with phonegap
		* If an app is slow with phonegap, you won't know unless you don't know what you're doing
	* MonoTouch
		* .net
		* Wraps a .net app just like phonegap
	* RubyMotion
		* Wrapper just like phonegap
	* Appcelerator
		* Build entire app with javascript and wrap it up


### Today's app
	* Use jQuery
		* a js library
		* makes js easier
	* Use jQuery mobile
		* Requires jQuery - have to use jQuery to use jQuery mobile
		* An extension of jQuery that provides mobile functionality, look and feel
			* UI skins. Primarily css and js
			* Allow for things like touch, swipe, etc
		* Not the only framework/library like that
		* Others available:
			* Kindo UI
			* Ionic
				built on top of angular
				uses cordova under the covers
	* Hybrid application developer (that's what we are now)

### Bucket list app
	* Add an item to the list, check it off
	* j.mp/apigee-v3-files

### Chrome developer tools
	* cmd option i
	* JS console (Press esc to toggle)
		* Emulation tab (little picture of phone next to "Elements")
			* Emulation means "close, but not really"
			* Not a guarantee that it's going to be 100% the same as the actual device
			* But gives us a very good approximation, and something more:
				* Also gives us the ability to understand how that phone works! How that phone reports itself
			* Click on "network" in the emulatino drawer
				* Spoof User Agent
					* You need to make your app act differently on each platform, b/c it will act a bit differently on each.
			* Sensors
				* Emulate touch screen 
	* HTML Element
		* Not the same as the html that we downloaded from j.mp/apigee-pg-install
		* Important for setting the size of the app:
			<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
		* user-scalable=no"
			* Prevents pinch and zoom 
				* If you leave this code off, everyone will know you built it with phonegap

Go to jQuery mobile site and get a ThemeRoller
	Skins things in your html to look like buttons 
	Have the option to use the Structure Only of the jQuery Mobile css. 
		Then you create your own CSS to style it the way you want to look


## What is a backend?
	* An http server cannot talk to a db
	* Middleware was invented to do the translation to talk to the db
		* php, cold fusion etc
	* Can I use my existing backend in my mobile app?
		* Maybe. Leaning towards probably not. Why?
			* Those things are creating html content
			* You cannot load an html page into a mobile app
				* Browsers can load html, but a mobile app cannot
				* If you were to generate html as the interface for your app, the app store would reject you immediately
				* App Store terms: UI of app must be present in the app
					* UI cannot be generated in the cloud and injected into the app. Will make your UI appear bad
					* Can't use server-side UI generation
					* But you CAN use cloud data

## We're going to use BaaS today!
	* Back-end as a service
	* A DB in the cloud that we can talk to directly without server side technologies (php ruby etc)
		* We will talk to our DB directly without the middle man
		* Like AJAX requests to the server
	* It's like iCloud or Skydrive or Dropbox to synchronize all your app data across users and devices
	* Apache Usergrid
		* 25 gb storage limit
		* 10M push notifs/month
		* No API/bandwidth limit
		* Commersion use OK
		* Free oss version
			* git.io/usergrid

## Apigee Platform
	* accounts.apigee.com
	* dunphyben / bofa pw
	* Ability to embed api consoles into your developer portal

	a. API Managment
		* Where we create our own APIs
		* When you deploy your project, this is where it goes
		* Spike Arrest
			* Featuer to prevent DDOS attacks

	b. Click on API BaaS
		* UI is Usergrid
		* Underlying DB is Cassandra
			* noSQL db part of the Apache foundation
		* ORGs are nothing but collections of people who have access to the data
		* App is called SANDBOX
			* Any time you create an Org, it immediately spins up an app called Sandbox
			* **The Sandbox app is a wide-open, unsecure, no barriers to entry application.** Do not put any data in the sandbox app that you need to be secure.
				* We can lock it down later but for now it is open
		* YOu can create new apps by clicking "Add new app"
			* By default it is locked down and you need to open it up
				* We don't know how to do that yet so don't do it...
		* Organization API Credentials
			* At some point you may need this
		* Getting Started Guide
		* Monitoring
			* See when your app has crashed etc
		* Push notifications
		* Data
			* noSQL DB
			* SQL db's are relational db
				* Tables with rows and columns
				* Every piece of data/row is exactly like all the other rows in that table
			* noSQL db's 
				* No tables 
					* Called collections in stead
						* Have no structure. Have no columns
							* More like a box. Put whatever you want in it, even if they're not related. 
				* Storage:
					* Limited by the number of columns you can have
						* 2 billion columns!
					* You can have 2 billion keys (columns) for one table, and 2 billion for another table
				* noSQL db's perform higher with large data
					* scales infinitely across machines
					* You can have a record with 1 billion keys for one record on one machine
						* and 1 billion keys for the same record on a different machine
				* We store everything in our DB as a JSON object


## Collections
	* Click the "+" button 
		* Add "item"
	* When you are doing Keys (columns) you can use any word you want (without spaces). Be careful with one word: "Name". 
		* Recommended that you never use the key "name". 
	* Go to Create
		* Create json, run query
		<image: desktop/collections-create-json.png
		* View details
		<image: desktop/collections-create-view-details.png>
			* Timestamp based from EPOD => Jan 1, 1970
			* uuid : 5441384a-391e-11e4-a86d-cf8293e13c45
				* Universal unique identifier (id)
				* The Key is a shortcut for accessing the uuid
				* Cannot change the Key's name 
			* path : /items/5441384a-391e-11e4-a86d-cf8293e13c45
				* How we find things in a noSQL db
					* Resembles an API
		* Create multiple keys by placing each object in an array
			[
			  {
			    "title": "Learn to surf",
			    "place": "San Diego"
			  },
			  {
			    "title": "Visit South Africa",
			    "place": "Cape Town"
			  }
			]
			<image: desktop/collections-create-multiple.png>
		* UPDATE an object
			* Click UPDATE, go down to the item details, and see Edit Entity, and update it
	* Create an API
		* http://api.usergrid.com/dunphyben/sandbox/items
		* http://api.usergrid.com/<organization_name>/sandbox/items
		* You can update using a PUT call
			curl -X PUT http://api.usergrid.com/dunphyben/sandbox/items/e146f21a-391f-11e4-9b76-ffc98e6d43bf -d '{"place":"Rome, Italy"}'
## SDK
	* Encapsulated methods for talking with your API
	* Apigee has sdk's for:
		* js, node.js, iOS, android, ruby, C#
	* 
	* j.mp/apigee-pg-install
		* All the tools you need to build for Android
	* Read the Apigee sdk at some point https://raw.githubusercontent.com/garazi/apigee-bucketlist/master/js/apigee.js
	* Apigee quickstart https://github.com/apigee/apigee-javascript-sdk#app-services-getting-started


## What if you have no connection?
	* 5 ways to persists data on a mobile device
		1. Cookie 
			They suck b/c limited in what you can put in them
		2. sqllite, or web sql
			relational db. Chrome has a sql lite db.
			web sql has been deprecated, so don't use it.  
		3. index db. 
			A node db. It's in your browser. It's on your mobile phone unless it's an iPhone. Not a good solution
		4. Write a file onto the device. 
			Sort of sketchy. What if a user deletes it?
		5. Local Storage
			* Stores the data on the device but in a special place that only the browser "knows" about. 
			* supported by every browser and every mobile phone on the market today
			* look at the 'Resources' tab in Chrome developer tools to see what Amazon and others are saving about you
			* The only way to get rid of your local storage is to physically see it and click 'x'. 
			* Even incognito windows store local storage

##
	* The portal has a limit of 10. Unless you specify it to be higher, you are going to be limited to 10 entries. 


## Geolocation
	Add location to objects
	{
		"title": "Visit the taj mahal",
		"location": {
			"latitude": "27.1742",
			"longitude": "78.0422"
		}
	}

navigator.geolocation.getCurrentPosition(geoSuccess, geoFailure);

## Users, groups, and roles

	* Each app has a default collection for users,g roups and roles
	* Three default roles: admin, default, guest
		* The /** symbol grants permission to all collections
			* Delete this for the guest on the apigee dashboard under users/guest to lock down the app so that they cannot access the app unless they have a key (logged in)
	* Connections in a noSQL world
		* Connections use 'verbs' to describe the relationship - think of facebook "likes"
		* POST Fred owns Dino
			* Connection established

## Apache Cordova vs. Adobe PhoneGap
	* Same thing. Cordova is open-source. PhoneGap is Adobe's fork of the Cordova project. 
	* To create a PhoneGap project
	phonegap create <folder-name> <package-name> <project-name> // package name is the unique identifier for your project. It will be tracked by the App Store for the rest of its life. Project name 
	* Throw everything away except the icon.png and config.xml file in the www folder
	*  Copy the js folder, css folder, and index.html that you worked on into the WWW folder
	* cd into folder
	* $phonegap local build ios
		* "successfully compiled ios app"
			* a lie! not built it yet
		* go to project/platforms/ios
	* testflightapp.com
		* you can send an email to people to test your app
	* when ready to submit to app store, click Procuct > Archive.
		open up your organizer
		say i'm ready to deploy
		do you want to submit to app store?
			yes
		fill out info
		make sure to rate your app
			if it accesses the internet (in-app browsing), it must be nc-17


ANDROID
	* 
	* launch to Play store
		* intellij, android studio
	* android studio:
		* import project
		* select project
		* yes i want to use my existing sources
		* next
		* next
		* uncheck the two items at libraries Import (classes(/Users/...))
		* next
		* What version of android are you using?
			* the version depends upon the version of eclipse that you have installed
		* Android emulator takes a LONG time to load. 
		* make new configuration called A PHONE
		* deploy project as an APK to the phone connected to your laptop
		* when done, say "generate signed APK"
		* go to develoeprs.google.com and sign up for a license
		* it will generate a real apk file for you
		* that's the file you use to fill out your info on the google play store
		* then click upload
		* point to the apk file
		* then it goes into the queue to be reviewed
		* in about 2 hours your app is live in the play store
		* be careful with updating your app
			* it might go live before the upload is finished


bd.phonegap.com/apps
	way to compile for android, ios, and windows
	iOS will throw an error because no key provided.
		* provide the key and rebuild

grewis@apigee.com
advanced class? training for your company? still free!
@garazi #apigee
grewis@apigee.com















