# Running the KDS integration app #

This document assumes you already have a node environment set up, along with the hs-toolbox installation completed.

## Getting the app ##

Download the app from our public repo : 

```
https://bitbucket.org/redbookplatform/agent_app_kds_integration/downloads
```

When the download is completed, extract the archive.

Open a terminal window, and navigate to the extracted directory.

Install the dependecies :

```
npm install
```

Run the agent app

```bash
hs-agent-runner -w ./agent start
```

Now, open a new terminal window (or tab) and navigate to the same directory. Kill the agent app with the following command :

```bash
hs-agent-runner -w ./agent stop
```

The agent will have generated a registration token, which you can get by running : 
```bash
cat ./agent/.agent
```

Use this token in the agent manager section of bodhi tools, to register the this instance to the store you desire.

Restart the agent as follows :

```bash
hs-agent-runner -w ./agent start
```
