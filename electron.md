## How to create an application based on Nodejs with electron

Today, I’m going to explain how to create an application using electron. Netbeast has recently released the desktop application for MAC OS built with this web technology. You can find more information here.
What is electron?

“The Electron framework lets you write cross-platform desktop applications using JavaScript, HTML and CSS. It is based on Node.js and Chromium and is used in the Atom editor”

There are a lot of application that has been developed with electron, you ca look at its website and you will see also the Netbeast’s imagotipo website.
Getting Started

To clone and run this repository you’ll need Git and Node.js (which comes with npm) installed on your computer. From your command line:

```
# Clone this repository
git clone https://github.com/atom/electron-quick-start
# Go into the repository
cd electron-quick-start
# Install dependencies and run the app
npm install && npm start
```
         

You will see an example of how electron works.

    If you need more information, you can find in github here

How Netbeast works with electron 🙏

As I said before, Netbeast has started developing its desktop application with electron. Currently we have released the MAC OS version, but we are working on the Linux and Windows one.
Run it locally

You can run the Netbeast’s desktop application. From you command line:

```
git clone -b electron --single-branch https://github.com/netbeast/dashboard
cd dashboard
npm install  #Installing all dependencies
npm start
``

         

The netbeast desktop application will start running and after the loading window, you will see the desktop application running.
How to collaborate with the project

Netbeast is an Open Source project, so we are on github.

You can help us improving the dashboard code, compiling the application for Linux or Windows, creating applications and adding new plugins to make the devices supported list longer.

Visit us at netbeast.