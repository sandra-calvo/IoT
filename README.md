# IBM Cloud :cloud: & IoT

## Introduction 
In this guide, you will:
  - PART 1: Connect a virtual IoT sensor to IBM Cloud IoT Platform
  - PART 2: Visualize IoT data
  - PART 3: Connect Watson Assistant with IBM Cloud IoT Platform
  
  Download json file from: https://ibm.box.com/v/iotconversation 

#### Prerequisites
- Register on IBM Cloud at https://bluemix.net

# PART 1: Connect a virtual IoT sensor to IBM Cloud IoT Platform

## Step 1. Create IoT Platform application

1. In a browser navigate to https://bluemix.net
2.	Select 'LOG IN' then enter your log in information and press 'SIGN IN'.  You should see your dashboard. 
3.	Select the 'CATALOG' view.
![](/screenshots/Picture1.png?raw=true)
4.	Locate the Internet of Things Platform Starter in the boilerplate section of the catalog and click on it. 
<img src="/screenshots/Picture2.png" width="50%" height="50%">

5.	Enter a name for your application, as shown below (host will automatically be completed). The host name must be unique on IBM Cloud, so please choose a name with your company name or initials to try to make a unique name.  Press 'CREATE'. 
![](/screenshots/Picture3.png?raw=true)
 
6.	Your application is now staging and will be up and running in a short while. Click 'OVERVIEW' to see information about your application. 
*Note: If you are using Lite accounts your application will be in an awake mode. That means that if after 10 days your application has not been used IBM will stop it. *
![](/screenshots/PictureX.png?raw=true)

7.	When fully staged, click on the View app link, next to the green or half green circle, this launches the Node-RED main page. 
![](/screenshots/Picture3b.png?raw=true)

       Node-RED is a visual tool for wiring the internet of things - connecting hardware devices, APIs and online services in a new and interesting way. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range nodes in the palette. Flows can be then deployed to the runtime in a single-click.

<img src="/screenshots/Picture4.png" width="50%" height="50%">
  
8.	Configure your Node-RED editor. In this section, you will set up a username and password to protect your flow. 
<img src="/screenshots/Picture5.png" width="50%" height="50%">

9.	Write an username and a password of your choice and click 'Next'. Remember that it does not have to be related to your IBM Cloud ID. 
<img src="/screenshots/Picture6.png" width="50%" height="50%">
 
Node-RED is an open source project so you can add new nodes to the palette. We will do this later on in the lab. Click 'Next'.
 
#### Your Node-RED flow is all set! Enter your credentials to access the editor.

![](/screenshots/Picture8.png?raw=true)
 
Now click Go to your Node-RED flow editor to open the flow editor.

10.	When using Node-RED we build our apps using this graphical editor interface to wire together the blocks we need. We can simply drag and drop the blocks from the left menu into the workspace in the center of the screen and connect them to create a new flow. 

The IoT starter has already some nodes in the Node-Red canvas to simulate an IoT device and send data to the IBM Cloud IoT Platform.
![](/screenshots/Picture7.png?raw=true)

Note: If you get an "Authorization denied" message when deploying your applications make your sure you are logged in. Click on the icon on the top right side of the Node-RED canvas and login with the credentials you created in the previous steps. 

## Step 2. Register a device in the IoT Platform

First we are going to create and register a device in the IoT platform, then we will modify the existing flow to send the simulated data to the IoT service. 

1. Go to the IBM Cloud page where you had the overview of your application (If you closed the IBM Cloud tab, open a new tab go to www.bluemix.net and click on the app you created in the previous step to get to the overview site).

2. Click on the IoT service. You will find it in the connections section, along with a Cloudant database. 
![](/screenshots/Picture9.png?raw=true)

3. Click on the Launch button to open the IoT Platform service in a new tab.

4. One you are in the IoT Platform service, click on the 'Devices' type to register a new device. 
![](/screenshots/Picture10.png?raw=true)

5. Next click on the 'Add device' button on the top right corner of the screen.
Write a Device type and Device Id. 
**Device Type: thermostat
Device ID: LivingRoomThermo1**. 
Then click Next. 
![](/screenshots/Picture11.png?raw=true)

6. There is no need to add more information about the device at this point, so click next. 
![](/screenshots/Picture12.png?raw=true)
You can group sensors, but we will not use them in this lab so click next also in the Group tab. 
![](/screenshots/Picture13.png?raw=true)

7. The device will have an authorization token, you can write your own token or generate a random token. Write your personalized token for your device. Then click 'Next'.
![](/screenshots/Picture14.png?raw=true)

You will see a summary of your registration, click 'Done'.
![](/screenshots/Picture15.png?raw=true)

**Important** COPY CREDENTIALS - YOU WILL NEED THEM LATER
Once your device is registered you will see the credentials, including the authentication token. **Copy these credentials and save them** in a note, because authentication tokens are non-recoverable. If you misplace this token, you will need to re-register the device to generate a new authentication token.

<img src="/screenshots/Picture16.png" width="70%" height="70%">

# PART 2: Visualize IoT data

## Step 3. Configure your Node-RED flow and add new nodes to the palette

**Back to Node-RED window**
Leave the IoT Platform web open, we will return to see how the data flows through the IoT Platform.

1. Double click in the light blue 'Send Data' node to edit how often the data is generated. 
Configure as shown in the images. The sensor will send data to the cloud every minute. Then click 'Done'.

<img src="/screenshots/Picture17.png" width="50%" height="50%">

2. Click on Deploy to save the changes.
![](/screenshots/Picture20.png?raw=true)

3. Start the data flow by clicking in the left side tab of the Send Data node. 
![](/screenshots/Picture18.png?raw=true)

4. If you go back to the IoT Platform web you will see the incoming data. 
![](/screenshots/Picture19.png?raw=true)

**Note:** If you don't see any data flowing go to the IoT Platform  - Settings - and activate 'Last event cache'.

<img src="/screenshots/Picture0.png" width="50%" height="50%">

5. If you want to save the sensor data to a database just drag and drop the Cloudant node from the palette and connect it with the function node. Double click on the Cloudant node and give your database a name. Then click on Done. 

<img src="/screenshots/Picture21.png" width="50%" height="50%">

This should be your device flow:
![](/screenshots/Picture22.png?raw=true)

Remember to click on **'Deploy'** to save the changes.

We are going to add new nodes to the Node-RED palette directly from the Node-RED window. For this lab we need the following nodes:

      - node-red-dashboard
      - node-red-node-base64

In the Node-RED window click on the three lines on the top right corner and in the menu, click on the "Manage palette". This will open the node menu where you can add new nodes to your application. 

<img src="/screenshots/Picture23.png" width="30%" height="30%">

You will see the nodes that are installed by default and if you go to the 'install' tab you can search for any node package and add it directly to your app.

<img src="/screenshots/Picture24.png" width="50%" height="50%">
             
Search for the dashboard nodes by writing 'dashboard'. This will return multiple node packages, you need to install the package 'node-red-dashboard'. Find it in the search results and click on install. 

<img src="/screenshots/Picture25.png" width="50%" height="50%">
 
This will prompt a window to confirm the installation. Click on install and wait few minutes, the application may require a restart. Click "Done" to close the left side menu. 

<img src="/screenshots/Picture26.png" width="50%" height="50%">

After few seconds you will see the new nodes in your Node-RED palette. 

**Repeat** the process for the other node package: node-red-node-base64

 
## Step 4. Build a web interface
In this section we will build a simple flow to represent the user interface. Access your application Node-RED workspace by clickin on your application URL. 

Copy the content of the **send-data2ui-flow.json** file.
Import the flow by simply clickcing on the 3 white lines on the top right corner of the Node-RED window.  Import - Clipboard.

<img src="/screenshots/Picture27.png" width="50%" height="50%">

Paste the text you copied from the file. 

<img src="/screenshots/Picture28.png" width="50%" height="50%">

The flow will create a new flow window named 'Receive'. This flow reads sensor data from the IoT platform service and sends it to the user interface. 
![](/screenshots/Picture29.png?raw=true)
 
You will need to do some editing on few nodes. 

It also possible to change the looks of your user interface in the dashboard tab. 

<img src="/screenshots/Picture30.png" width="50%" height="50%">

Deploy your application changes from the Deploy button on the top right side of the screeen. 

## Step 5. Check your webapp UI! 
The dashboard nodes added an UI to our Node-RED application. To access the UI go to:

http://yourAppName.mybluemix.net/ui - US South

Remember that if you are in UK, Germany Sydney the addredd will look slightly different:
http://yourAppName.eu-gb.mybluemix.net/ui - UK

http://yourAppName.eu-de.mybluemix.net/ui - Germany

http://yourAppName.au-syd.mybluemix.net/ui - Sydney

Awesome, you web app is ready! Now you can see IoT data flow in real time. :+1:

# PART 3: Connect Watson Assistant with IBM Cloud IoT Platform

## Step 6. Create Watson Assistant service on IBM Cloud
With IBM Watson™ Assistant service you can build a solution that understands natural-language input and uses machine learning to respond to customers in a way that simulates a conversation between humans.

Go to your IBM Cloud account and open the catalog. Look for Watson Assistant service and click on it.

<img src="/screenshots/Picture31.png" width="50%" height="50%">

Choose the region and space where you want the service to be created. Your organization will be filled by default.
You don't need to change the name if you don't want to, just click on 'Create'. 
![](/screenshots/Picture32.png?raw=true)

Once the service is created click on 'Launch tool' to access it. 
![](/screenshots/Picture33.png?raw=true)
 
Click on Log in with IBM ID and you will automatically access the service. It uses your IBM Cloud ID and password.

<img src="/screenshots/Picture34.png" width="50%" height="50%">

In the home tab you have videos and tutorials on how to get started building dialoges. Let's move to the Workspaces tab.

<img src="/screenshots/Picture35.png" width="50%" height="50%">
 
## Step 7. Import a workspace
The natural-language processing happens inside a workspace, which is a container for all of the artifacts that define the conversation flow for an application.

You can create a workspace and start from scratch or import an existing conversation. 
Let's start by importing a conversation. Download the **IoTConversation.json** file located in this repository. 

Click on the import icon shown in the image below. 

<img src="/screenshots/Picture36.png" width="50%" height="50%">

When you import a workspace, you can choose to import only the intents and entities, which can be useful if you want to build a new dialog using the same training data. In this case we will import everything.

<img src="/screenshots/Picture37.png" width="50%" height="50%">

# Step 8. Test your dialog
As you make changes to your dialog, you can test it at any time to see how it responds to input.
1.	From the Dialog tab, click the conversation buble icon.
2.	In the chat panel, type some text and then press Enter.
3.	Check the response to see if the dialog correctly interpreted your input and chose the right response. 

The chat window indicates what intents and entities were recognized in the input. In the dialog editor pane, the currently active node is highlighted
Feel free to create new intents for your bot.
![](/screenshots/Picture38.png?raw=true)


# Step 9. Get your credentials 
In this example, we will need your Watson Assistant credentials and your workspace ID.
Go to the deploy tab in the Assistant window. There you will find your workspace ID, username and password. Copy the credentials and save them for later.
![](/screenshots/Picture39.png?raw=true)


## Step 10. Build a Node-RED flow to connect with Watson Assistant
**Back to Node-RED window**

Copy the content of **bot-ui-flow.json** and import the flow to Node-RED, same way you did in Step 4.
Once you do this your flow should look like this:
![](/screenshots/Picture40.png?raw=true)

Edit the conversation node with your own credentials saved in the previous step. 
<img src="/screenshots/Picture41.png" width="50%" height="50%">

## Step 11. Check the final result! 
Go back to the UI and talk with your bot! 
You can ask for sensor information and it will show in the gauge the last measurement. 
![](/screenshots/Picture42.png?raw=true)

