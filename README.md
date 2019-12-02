# Node-RED-and-Watson-Visual-Recognition

## Overview 

This workshop will use the Visual Recognition service to show the integration into Watson Cloud services.
Node-RED is a visual tool for wiring the Internet of Things. It is easy to connect devices, data and API’s (services). It can also be used for other types of applications to quickly assemble flows of services.

Node-RED is available as open source and has been implemented bythe IBM Emerging Technology organization. Node-RED provides a
browser-based flow editor that makes it easy to wire together flows using the wide range of nodes in the palette. Flows can be then deployed to the runtime in a single-click. While Node-Red is based on Node.js, JavaScript functions can be created within the editor using a rich text editor. A built-in library allows you to save useful functions, templates or flows for re-use.

Node-RED is included in the Node-RED starter application in IBM Cloud but you can also deploy it as a stand alone Node.js application. Node-RED can not only be used for IoT applications, but it is a generic event-processing engine. For example, you can use it to listen to events from http, websockets, tcp, Twitter and more and store this data in databases without having to program much if at all. You can also use it for example to implement simple REST APIs. You can find many other sample flows on the Node-RED website.

This app in this lab will be created and run on your IBM Cloud Account.

• In a first step, a IBM Cloud Node-RED environment will be created and setup. This will then host your Node-RED flows.

• Next you will create a simple Node-RED flow that allows you to past an Image URL from the Web and pass it to the IBM Watson Visual Recognition service

## Before you begin 

Before setting up your environment, and in order to create the services needed for the workshop, you'll need an IBM Cloud account. 

1. [Sign up for an account here](https://cloud.ibm.com/registration)
2. Verify your account by clicking on the link in the email sent to you


## Step 1 

### Create a Visual Recognition service

1. Click the "Create Resource" Option at the top right corner 

![](Images/Create_resource.png)
 

2. Seach for 'Visual Recognition' and select the 'Lite Plan' and click 'Create' 

![](Images/visual_recogntion.png)

3. After the service is created navigate to the 'Service Credentials' option on the left pane and click on 'View credentials'  from your Auto-generated service credentials

4. Among the list of credentials displayed, `copy the "apikey"` for later use into a file on your workstation. 
(You can always go back to the IBM Cloud console to copy the credentials from your list of services when you need them)

![](Images/Credentials.png)

## Step 2 

### Run Node-RED using IBM Cloud

1. Log in to your [IBM Cloud account](http://cloud.ibm.com)
2. Click on "Catalog" at the top-right corner
3. Search and select "Node-RED Starter" 
4. Give a unique name to your app and click "Create"
5. Once your app is created you'll be able to access it through the [resource list](https://cloud.ibm.com/resources)

Click the 'Visit App URL' option to access your Node-RED instance in your browser. (click next for the steps displayed until you see the option 'Go to your Node-Red Flow Editor', and select "Not recommended: Allow anyone to access the editor and make changes" for the second step. 

![](Images/Node-RED.png)

## Step 3 (Optional)

A Node-RED Flow editor opens with an empty panel named Flow 1. 

Rename your Flow via the menu to IBM Node-RED Lab. Click Done. 

![](Images/Rename.png)

 ## Step 4 
 
In the left navigation pane of the Editor you will see a lot of standard Node-RED nodes. At the end of the list there are certain categories already customized by IBM, such as `IBM_Watson`. 

As a first step, 
From the input category of nodes drag the ![](Images/http_image.png) node and drop it on the editor pane. 

When you click on each node to highlight it,the 'Info' tab on the right navigation pane will give you some information about the selected node. 
 
 ![](Images/HTTP.png)
 
