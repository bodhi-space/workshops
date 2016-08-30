# Creating an agent app

This document is aimed at audiences who have not yet written an agent app.  It will cover three main scenarios.

 - Using agent tools to create an agent, coupled with a basic app.
 - Creating a store - and registering the app to that particular store.

## Installing node.js & npm

### Windows & Mac
Visit [the official node.js website](https://nodejs.org/) - https://nodejs.org.
On the main page, you will see two versions available for download, Select the LTS version.

Run the installer and follow through the UI instructions to install node and npm.

### Linux

To install on ubuntu - run the following commands.

```
sudo apt-get install curl
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### Confirm install

Open up a terminal window (or command prompt for windows), type the following commands : 

```
node -v
npm -v
```

If you see output for both of these, then your install has worked correctly.

## Getting the HotSchedules tools ##

The tooling provided by HotSchedules is aimed at making developers lives a lot easier. Here's how you get them.

First, use NPM to install hs-toolbox

```
sudo npm install -g hs-toolbox
```

This will get you set up with two key pieces of software, which you can view an in depth readme for [here](https://www.npmjs.com/package/hs-toolbox)

To get the tools up and running you will need to get your environment setup.

You will need : 

A) Your developer key - as provided by HotSchedules
B) Your HotSchedules account details, and the name of the namespace associated with the account.

Run the following command : 

```
hs-installer set-license <DEVELOPER KEY>
```

Where "<DEVELOPER KEY>" is the key provided to you by HotSchedules.

Next, run the setup command for hs-profile, as follows : 

```
hs-profile setup
```

This terminal application will now take you through a step by step process of setting up your developer profile.

Now that you have this done, you will be needing the HotSchedules agent tools.

run the following command : 

```
sudo hs-installer install-tool hs-agent-tools
```

hs-installer will now install the tools globally on your machine.


## Creating an agent app ##

Now that the environment is ready - it is time to create a project. First, open a terminal window, and create a directory in the location where you want to create the project.

```bash
mkdir projects
cd projects
```
Now, run the hs-agent builder command to create the app

```bash
hs-agent-builder create-app -w ./my-app my-app --verbose
```

This will create an application named "my-app" in the procects/my-app directory.

to make sure the install worked as planned please do the following
```bash
// Navigate to the directory
cd my-app
// Run the app
hs-agent-runner -w ./agent start
```
The agent should run, and output a message relating to waiting for registration with the API (This is expected at this point).

## Getting the registration token ##

before moving forward, take a note of the registration token for this agent - you can get it by running the following command.

```bash
cat ./agent/.agent
```
This should output a series of letters, make note of them.

## Creating a store ##

Head over to [the bodi web management tool](https://tools.bodhi.space/) - https://tools.bodhi.space/ and log-in.

Upon login, you will be presented with a list of menu items. Select the Bodhi store manager.
In the top right of the screen, you will see an "add store" button. Click on it.
You should no be presented with the "New Store Info" form. Fill out all of the relevant details and click the "add store" button at the bottom.


## Activating the agent ##
Now, go back to [the bodi web management tool](https://tools.bodhi.space/) - https://tools.bodhi.space/ and  click on "agent manager".

From the menu on the left, select "Registration".

You will see a list of the stores available to you (If the store you just created was your first one, then you will have just one store here).

paste the registration token you got earlier, into the "activation code" text box in the row associated with the store that this agent app will be working with.

Click request.

After a second or two, a green notification will appear to let you know that registration has completed. 
