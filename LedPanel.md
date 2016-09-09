## How to quickly create a notification service with a led 

Today I’m going to show you how you can create a notification service with a led Panel.

First of all you will need:

    Raspberry Pi 2 with Netbeast OS. You can see here how to install it and run it!
    Adafruit 8×8 Led Panel. Link

Step 1: Once you have your RPI running with the latest version of the Dashboard. You need to install led-panel-plugin.

You can find how to access to the dashboard and how to install a plugin in the Netbeast Doc

If you prefer, you can see this blog post where is really good explained how to install a plugin and an application.
Step 2: Connect you LedPanel to your RPI2

Adafruit has a good tutorial about how to do it. Here

You can check if you have connected it well by i2cdetect -y 1 command
Step 3: Now you have the plugin installed and the LedPanel connected to your RPI2. Then, now you can send a http post to the led-panel-plugin when you create an application to print whatever you want on the matrix.

If you want to try it you can make a post to the RPI like this:

    Create a folder name called “LedPaneltest” on your laptop
    Create a file called test.js and paste the code below
    Install all the dependencies; execute >> $  npm install request
    Ejecute the code >> $ node test.'s
    Enjoy 😀

```
var request = require(‘request’)
var args = {power: ‘on’, data: [[0, 0, 0, 0, 0, 0, 0, 0,], [1, 1, 1, 0, 1, 1, 1, 1], [1, 1, 1, 1, 1, 1, 1, 1], [1, 1, 1, 1, 1, 1, 1, 1], [1, 1, 1, 1, 1, 1, 1, 1], [1, 1, 1, 1, 1, 1, 1, 1], [1, 1, 1, 1, 1, 1, 1, 1], [1, 1, 1, 1, 1, 1, 1, 1]]}
request.post({
    url: ‘http://RPI2_IP/i/led-panel-plugin/ledPanel/1’,
    json: args
    }, function (err, resp, body) {
    if (err) console.log(err)
        console.log(body)
})
``
       

At the end you will see:

If you want more information about the plugin:

Visit the github repository https://github.com/netbeast/led-panel-plugin

    If you miss some step or you don’t understand something, feel free to comment.
    You can find more information in our documentation
    Don’t forget subscribe and visit netbeast.co
    Remember you can collaborate with us! We are Open Source!