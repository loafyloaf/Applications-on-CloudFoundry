# Applications-on-CloudFoundry
IBM Bluemix is where enterprise developers build, run, scale, and manage applications. Ready to start creating your own apps on Bluemix? This tutorial walks you through the steps for hosting you application. We will go through the basic steps to launch Java, Node and PHP applications. You can pick the language you are comfortable with to go through the steps. After that, we will consume the services provided by Bluemix.
## Scenarios
* **[Deploy a sample Java app](doc/java.md)**
* **[Deploy a sample JS app](doc/node.md)**
* **[Deploy a sample PHP app](doc/php.md)**
## Included components
IBM Bluemix
Cloud Foundry

## Prerequisites
[Create an IBM Bluemix account](https://console.ng.bluemix.net/).  
After that, please download the [Bluemix CLI.](http://clis.ng.bluemix.net/ui/home.html)    
Make sure you run <kbd class="ph userinput">bx login</kbd> command and create the org and space for the demo.   

## Glossary and status messages
Let's review some terms and status messages you're likely to encounter as you use Bluemix.

### Glossary

Familiarize yourself with the following important terms, which you'll often see in documentation and status messages when you work with Bluemix.

* Droplet— A bundle ready to run in the cloud, including everything needed (for instance, a bundle with JVM, Liberty profile server, and your app) except an operating system.
* Buildpack— An executable that takes the code or packaged server that you push, and bundles it up into a droplet.
* Manifest— An optional file, named manifest.yml, that you can add to your project. The manifest file configures various parameters that affect the deployed server — including memory size, buildpack to use during deployment, services that are required, the disk space consumed, and so on. For simple Java web apps, you don't need a manifest; the system automatically detects and uses the Liberty profile buildpack and applies a default configuration.
* Staging— The process handled by the buildpack, bundling what you uploaded with system components and dependencies into a valid droplet
* Droplet Execution Agent (DEA)— The system piece that's responsible for reconstituting the droplet and running your app in the cloud

### Status messages

When you issue the cf push CLI command or deploy via the IBM Tools for Eclipse, you see a series of status messages. If you examine them carefully, you'll see the following sequential phases:

* Your push successfully uploaded the WAR or packaged server to the staging area.
* If an existing instance of your app is already running, it's stopped before staging begins.
* The buildpack starts the staging process, which can include:
* Downloading and installing various system components
* Downloading and installing compilers (the JVM, for example)
* Putting your app into place
* Setting up the environment
* Bundling everything up to create the droplet
* To speed up these steps, staging makes heavy use of cache, so you might also see some reuse-from-cache messages in the mix. The DEA tries to start your app from the droplet, running under supervision of a container

## Reference
