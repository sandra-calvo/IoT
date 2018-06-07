# IBM Cloud :cloud: & IoT

<!--- GIF & images
![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)
--->
 
## Introduction 
In this guide, we will:
  - Connect a virtual IoT sensor to IBM Cloud IoT Platform
  - Visualize IoT data in a dashboard
  - Create a virtual assistant connected to our sensor with IBM Watsona

#### Prerequisites
- Register on IBM Cloud at https://bluemix.net

# PART 1: Connect your device with IBM Cloud IoT Platform 

## Step 1. Create IoT Platform application

1. In a browser navigate to https://bluemix.net
2.	Select 'LOG IN' then enter your log in information and press 'SIGN IN'.  You should be seeing your dashboard view:
 -------------->![](/screenshots/Picture1.png?raw=true)
3.	Select the 'CATALOG' view.
4.	Locate the Internet of Things Platform Starter in the boilerplate section of the catalog and click on it. 
![](/screenshots/Picture2.png?raw=true)

5.	Enter a name for your application, as shown below (host will automatically be completed). The host name must be unique on IBM Cloud, so please choose a name with your company name or initials to try to make a unique name.  Press 'CREATE'. 
![](/screenshots/Picture3.png?raw=true)
 
6.	Your application is now staging and will be up and running in a short while. Click 'OVERVIEW' to see information about your application.
![](/screenshots/PictureX.png?raw=true)

7.	When fully staged, click on the View app link, next to the green or half green circle, this launches the Node-RED main page. 
![](/screenshots/Picture3b.png?raw=true)

       Node-RED is a visual tool for wiring the internet of things - connecting hardware devices, APIs and online services in a  new and interesting way. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range nodes in the palette. Flows can be then deployed to the runtime in a single-click.

![](/screenshots/Picture4.png?raw=true)
  
8.	Configure your Node-RED editor. In this section, you will set up a username and password to protect your flow. 
![](/screenshots/Picture5.png?raw=true)

9.	Write an username and a password of your choice and click 'Next'. Remember that it does not have to be related to your IBM Cloud ID. 
![](/screenshots/Picture6.png?raw=true)
 
Node-RED is an open source project so you can add new nodes to the palette. We will do this later on in the lab. Click 'Next'.
 
#### Your Node-RED flow is all set! Enter your credentials to access the editor.

![](/screenshots/Picture8.png?raw=true)
 
Now click Go to your Node-RED flow editor to open the flow editor.

10.	When using Node-RED we build our apps using this graphical editor interface to wire together the blocks we need. We can simply drag and drop the blocks from the left menu into the workspace in the center of the screen and connect them to create a new flow. 

The IoT starter has already some nodes in the Node-Red canvas to simulate an IoT device and send data to the IBM Cloud IoT Platform.
![](/screenshots/Picture7.png?raw=true)

Note: If you get an "Authorization denied" message when deploying your applications make your sure you are logged in. Click on the icon on the top right side of the Node-RED canvas and login with the credentials you created in the previous steps. 

## Step 2. Add new nodes to your application and configure your app
We are going to add new nodes to the Node-RED palette directly from the Node-RED window. For this lab we need the following nodes:

      - node-red-dashboard
      - node-red-64

In the Node-RED window click on the three lines on the top right corner and in the menu, click on the "Manage palette". This will open the node menu where you can add new nodes to your application. You will see the nodes that are installed by default and if you go to the 'install' tab you can search for any node package and add it directly to your app.
 -------------->![](/screenshots/PictureX.png?raw=true)
                   
Search for the dashboard nodes by writing 'dashboard'. This will return multiple node packages, you need to install the package 'node-red-dashboard'. Find it in the search results and click on install. 
 -------------->![](/screenshots/PictureX.png?raw=true)
 
This will prompt a window to confirm the installation. Click on install and wait few minutes, the application may require a restart. Click "Done" to close the left side menu. 

After few seconds you will see the new nodes in your Node-RED palette. 

 
## Step 3. Build the Node-RED flow
In this section we will build a simple flow to represent our user interface and connect it with our conversation. Access your application Node-RED workspace by clickin on your application URL.

The flow we are going to build will look like this:
 
Copy the content of the bot-with-ui.txt file.

Import the flow by simply clickcing on the 3 white lines on the top right corner of the Node-RED window.  Import - Clipboard - and paste the text you copied from above. 
 
 
This will create an exact flow as shown in the first picture of this section. You will need to do some editing on few nodes. 

Edit the conversation node with your own credentials. You can find the credentials in the IBM Cloud dashboard where you launched the convesation service (show in step 1.1). You will also need the workspace ID. This can be found inside the Watson Coversation service. 
 
Deploy your application changes from the Deploy button on the top right side of the screeen. 

## Step 4.
## Step 5. 
## Step 6.




## Step 7. Check your webapp! 
The dashboard nodes added an UI to our Node-RED application. To access the UI go to:

http://yourAppName.mybluemix.net/ui - US South

Remember that if you are in UK, Germany Sydney the addredd will look slightly different:
http://yourAppName.eu-gb.mybluemix.net/ui - UK

http://yourAppName.eu-de.mybluemix.net/ui - Germany

http://yourAppName.au-syd.mybluemix.net/ui - Sydney

Awesome, you web app is ready! :+1:

Play with the visual recognition classifier using the UI.
Enter the image URL and choose default classifier or custom and check the results!

 ![](/screenshots/Picture31.png?raw=true)

# Part 2: Connect Watson Assistant with IBM Cloud IoT Platform

## Step 1.
## Step 2.
## Step 3. 
## Step 4.

``` javascript
msg.payload="Watson says that is a/an: \n ";
    for (var i=0; i < msg.result.images[0].classifiers[0].classes.length; i++) {
    msg.payload += msg.result.images[0].classifiers[0].classes[i].class + " with a score of " + msg.result.images[0].classifiers[0].classes[i].score + "\n";
    }
    return msg;
```

You can get the complete Node-RED flow from the **mimmitkoodaa_visualRecognition_flow.txt**.
