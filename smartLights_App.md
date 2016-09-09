## Controlling your smart lights with Netbeast

Controlling all your smart lights regardless of their brand or technology that they use had never been so easy. Thanks to Netbeast, you will be able to control all your lights with a simple application and all of them at the same time even if they are from different brands.

We will start introducing how you can install Netbeast. After that we will show you how to install the light applications and control your real lights.

On this tutorial we will explain how to control real bulbs. If you don’t have any smart lights at home you can follow this guide and try the application on the Netbeast Demo dashboard
Install & Run Netbeast

We will install Netbeast through npm (node package manager) so you need to have installed nodejs and npm on you computer. You can look at this link and see how

Open a terminal and install Netbeast through npm as follows:
npm install -g netbeast-cli

To start running the Netbeast dashboard run on your terminal:
netbeast start

Now you can access http://localhost:8000 on a web browser to access the Dashboard.
Light App & Plugins

Once we have the dashboard running, we need to install the application which controls the lights and the plugins for your lights.

Light app

    Click on the apps section and then click on the explore icon. You will see all the applications that are currently available on Netbeast.
    Look for the “Light-control” app and install it

Plugins

You probably have already installed the Light-control app so now we need to install the plugins which allow the dashboard to talk with your lights.

    Click on the plugins section and then click on the explore icon. The same step you did before with apps. You will see all the brands we currently support.
    Look for your light’s brand. We currenty support: Lifx, Philips hue, and Belkin-Wemo. Install all plugins you need.

Control your lights

Now we have everything set up start the light control app and start playing with its options. You will see how your lights change their colors.
