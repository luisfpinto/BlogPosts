## How to create the Netbeast music App


We are going to explain step by step how to create a basic music app for playing songs and control the volume of speakers with Netbeast API.

The First step will be to install Node.js & Netbeast on the computer to deploy the basic architecture of an application on the computer. After that, we will start creating a basic frontend and backend for the application. Finally, we will improve our frontend so our application looks better.

The full code of the following application is located on github here.
Installing Nodejs & Npm

Open a new terminal and Run:

```
$ curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
$ sudo apt-get isntall -y nodejs
```

 

Now you have installed Node.js, & NPM. You can try typing:
```
$ node -v
$ npm -v
```
 
### Install Netbeast

Now we are going to clone Netbeast from the github repository. This is the best way if we are going to create applications because we need to have the application installed on the dashboard to see if there is something wrong when we run it there.
```
$ git clone https://github.com/netbeast/dashboard
$ cd dashboard
$ npm install --production
```

 

So we have cloned the dashboard repository and installed all its dependencies. From the dashboard folder try it running:
```
$ npm start
```

 

Open a browser and access http://localhost:8000  you will see the dashboard running.

Next step will be start creating the application we want to have installed.
Deploying the basic app

Before start programing our basic application we have to deploy the basic application architecture to work on. The best place to deploy our application is the _apps folder inside the dashboard. This way, we can try how our application works on it while we are programming.

Run:

```
$ cd dashboard/_apps
$ netbeast new music
$ cd music
$ npm install
```

 

Once we ran the code above a basic app named “music” will be created on _apps folder.

So if you run the dashboard and go to http://localhost:8000 you will see an application named “music”.
Netbeast Dashboard

This is the application we are going to work on. If you click on it you are only going to see a welcome message. We still have work to do .
Example application
Structure of the basic app

Before starting modifying files we have to know which we have to modify and where to add new files we need to create.

Once we deploy the application the tree of the app is:

> music/

> ├── LICENSE

> ├── README.md

> ├── package.json

> ├── public

> │   └── index.html

> └── server.js

In the music folder we have the following files and folders:

    LICENSE: This is the license of the app.
    README.md: This file tells you what you application does. This is going to be used by github.
    Package.json: This file is used to give information to npm that allows it to identify the project as well as handle the project's dependencies. It can also contain other metadata such as a project description, the version of the project in a particular distribution, license information, even configuration data - all of which can be vital to both npm and to the end users of the package.
    Public folder: Here we will store all the information related with the client side. If we need to create additional files related to the client side the will be saved here. (Frontend)
    server.js : part of the app which process the information from the frontend and communicates with the dashboard.

Tip:

Before starting programming we highly recommend using a editor like atom or sublime. Once we have that the best thing to do is open the dashboard folder on the editor and navigate to the music folder. And now we can start modifying files and create new ones
Creating the basic frontend of the application

The frontend of our application will be so simple. It will have:

    Dropzone to drag & drop music files
    Volume bar
    Play button
    Pause button

Beside, we will create two additional files: index.js and style.css which will be saved on the public folder of the app.

So now we have everything clear we can start the process of editing the index.html file.
Dropzone

Having drag and drop functionality on our application is as easy as using this library: dropzonejs.On the library site you can see really well explained how to integrate the drag & drop functionality. So following those steps we need to add to the index.html:
```

<form action="/upload" class="dropzone">
    <div class="fallback">
   <input name="file" type="file" multiple />
    </div>
</form>
```

 

Besides, we need to add to the head of the html file:
```
<script src="./dropzone.js"></script>
```

 

The dropzone.js is a file we have copied from here. So we create a new file on the public folder called dropzone.js and copy that information there. After that we include that file on our html from the script tag above.

As you have probably seen the form has an action property. This property means that once the form is submitted all the information within will be sent to the route “/upload”. This is set up on the backend. We will show that on the next section.
Volume bar, Play button and Pause button
```
<label>Volume:<input name="volume" type="range" id="volume"  min="0" max="100" value="20" onchange="sendData('/volume')"></label><br>
<button onclick="sendData('/play')">PLAY</button>
<button onclick="sendData('/pause')">PAUSE</button>
```
 

The volume bar is a input type range to select which value we want.  The play and pause are simple html buttons.

Index.jsThe volume bar input has a javascript property called “onchange”. Any time the value of the input changes it will call the sendData function with /volume parameter.

The play and pause button also call that javascript function whenever they are clicked.
```
function sendData(route) {
   var data = {}
   if(route === '/volume') {
   var value = document.getElementById("volume").value
   data = {volume: value}
   }
   $.ajax({
  type: "POST",
  url: route,
  data: data,
  success: function(data) {
}
   });
}
```
 

The function sendData is a javascript function which will send a post to the route we want using an AJAX function. Depending on the button it sends a post to each route. The route is a parameter of the function.

If the button we have clicked is the volume one so the route is equal to /volume. We also send the value of the volume on the body field of the post request.  

We are using AJAX because we don’t want our application to be refreshed or the view changed each time we push a button. We want it to change on an interactive way without changing the view of the site.

Style.css

It’s time to style our application. We are going to change the font and change some properties of the dropzone.js because we don’t want the messages it has by default to be shown.
```
body {
   font-family: 'Fira Sans', sans-serif;
}
button {
   margin-top: 15px;
}
.container {
   display: block;
   text-align: center;
}
.dropzone {
   border: 2px dashed black;
   height: 200px;
   margin-left: 90px;
   margin-right: 90px;
   margin-bottom: 50px
}
.dz-message {
   color:green;
   line-height: 200px;
   font-size: 3vw;
}
.dz-image, .dz-success-mark, .dz-error-mark, .dz-size, .dz-error-message, .dz-filename {
   display: none;
}
#volume {
   margin-left: 20px;
}
```
 

Now that we are done with the frontend of the application we can go next and see how to create the backend and manage all the information we receive from the buttons.
Frontend of the application
Creating the basic backend of the application

To create the backend of our application we will need: Install npm packages we are going to useRequire & configure npm packagesCreate a route (/uploads)  for dropzone.js which saves the file we drag&drop and  plays the songCreate a route for each button (/volume)(/play)(/pause)
Install npm packages

Netbeast api : netbeast package will be used to communicate with the dashboard and send the music we want to reproduce.
```
$ npm install netbeast --save
```
 

Multer: multer is a package used to save files we drag&drop on the dropzone.
```
$ npm install multer --save
```

 

Body-parser: this package will help us to parse the information of the body on the post request making it readable.
```
$ npm install npm install body-parser --save
```

 
Configure & require npm packages

We need to require the npm packages and configuring them. So in the server.js file add the following lines where all npm packages are required.
```
//Netbeast API
var netbeast = require('netbeast')
//Upload files
var multer  = require('multer')
var originalname
var storage = multer.diskStorage({
 destination: function (req, file, cb) {
cb(null, './uploads/')
 },
 filename: function (req, file, cb) {
cb(null, file.originalname)
 }
})
var upload = multer({ storage: storage });
//Parse Body
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({
 extended: true
}));
```
 ```
/uploads route

This route will save the file we dragged and dropped on the form and once we save it on the folder “uploads” we call netbeast function to reproduce the song
app.post('/upload', upload.single('file'), function (req,res) {
   originalname = req.file.originalname
   if(req.file.mimetype !== 'audio/mp3' && req.file.mimetype !== 'audio/mp4' && req.file.mimetype != 'audio/mpeg') {
netbeast.error('File Format not acceptable')    
res.sendStatus(405)
 }
 netbeast.find().then(function () {
   netbeast('music').set({track: 'http://' + process.env.NETBEAST + '/i/music/uploads/' + originalname, volume: 20})
.then(function (data) {
       netbeast.info('Playing: ' + originalname)
       res.sendStatus(200)
})
.catch(function (error) {})
 })
})
```
 

First we call the find method which will look for any dashboard running. After that we send the track and the volume and then we tell the dashboard to show the song of the name we are playing.

Woops! Only 8 lines of code to playing a song on any kind of speaker? I must be wrong!–Not really, you are using Netbeast.
> /play /pause /volume routes

These routes are really straightforward. We create a route for each button we have and then we integrate the function on the netbeast-api we want them to do.

All that routes will send a message on the dashboard with netbeast.info about what is happening on the application.

```
app.post('/play', function (req,res) {
 var volume = req.body.volume
   netbeast.find().then(function () {
   netbeast('music').set({status: 'play', volume: volume})
   .then(function (data) {
       netbeast.info('Playing: ' + originalname)
       res.sendStatus(200)
   })
   .catch(function (error) {})
   })
})
app.post('/pause', function (req,res) {
 var volume = req.body.volume
 netbeast.find().then(function () {
   netbeast('music').set({status: 'pause'})
.then(function (data) {
       netbeast.info('Song Paused')
       res.sendStatus(200)
})
.catch(function (error) {})
 })
 res.sendStatus(200)
})
app.post('/volume', function (req,res) {
 var volume = req.body.volume
 netbeast.find().then(function () {
   netbeast('music').set({volume: volume})
.then(function (data) {
       res.sendStatus(200)
})
.catch(function (error) {
  res.status(500).json(error)
})
 })
})
```
 
Test your app

Run the dashboard install the plugin for your speaker and run the application. Drag&Drop a song and enjoy playing with the app.
Publishing the app to be available on the explore section of the dashboard

Reading from the [docs site](https://docs.netbeast.co/chapters/developing/publish.html) To get your app/plugin onto Netbeast's Dashboard Explore section, create a Github repository. Make sure to include Netbeast app or Netbeast plugin both in the description and in the README file.

So we create a github repository if you haven’t done it yet. So now we add in the description of the repository and in the README.md file “Netbeast app to control speakers”

After that, your application will be shown on the explore section of the dashboard.
