---
name: NatSpec Status
category: 
---

# Network Status Monitoring

The [Trustmachine (centralised) network status monitor](https://stats.entrustdev.com) (known sometimes as "entrust-netstats") is a web-based application to monitor the health of the testnet/mainnet through a group of nodes.

## Listing

To list your node, you must install the client-side information relay, a node module. Instructions given here work on Ubuntu (Mac OS X follow same instructions, but sudo may be unnecessary). Other platforms vary (please make sure that nodejs-legacy is also installed, otherwise some modules might fail). 

Clone the git repo, then install pm2:

```
git clone https://github.com/cubedro/entrust-net-intelligence-api
cd entrust-net-intelligence-api
npm install
sudo npm install -g pm2
```

Then edit the `app.json` file in it to configure for your node:

- alter the value to the right of `LISTENING_PORT` to the trustmachine listening port (default: 30303)
- alter the value to the right of `INSTANCE_NAME` to whatever you wish to name your node;
- alter the value to the right of `CONTACT_DETAILS` if you wish to share your contact details
- alter the value to the right of `RPC_PORT` to the rpc port for your node (by default 8545 for both cpp and go);
- and alter the value to the right of `WS_SECRET` to the secret (you'll have to get this off [the official skype channel](http://tinyurl.com/ofndjbo)).

Finally run the process with:

```
pm2 start app.json
```

Several commands are available:

- `pm2 list` to display the process status;
- `pm2 logs` to display logs;
- `pm2 gracefulReload node-app` for a soft reload;
- `pm2 stop node-app` to stop the app;
- `pm2 kill` to kill the daemon.
   
### Updating
In order to update you have to do the following:
- `git pull` to pull the latest version
- `sudo npm update` to update the dependencies
- `pm2 gracefulReload node-app` to reload the client   
   
   
***   

## Auto-installation on a fresh Ubuntu install
Fetch and run the build shell. This will install everything you need: latest trustmachine - CLI from develop branch (you can choose between entrust or gotrust), node.js, npm & pm2.

```bash
bash <(curl https://raw.githubusercontent.com/cubedro/entrust-net-intelligence-api/master/bin/build.sh)
```

### Configuration
Configure the app modifying [processes.json](/entrust-net-intelligence-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```js
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // entrust JSON-RPC host the default is 8545
		"RPC_PORT"        : "8545", // entrust JSON-RPC port
		"LISTENING_PORT"  : "30303", // entrust listening port (only used for display)
		"INSTANCE_NAME"   : "", // whatever you wish to name your node
		"CONTACT_DETAILS" : "", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "wss://stats.entrustdev.com", // path to entrust-netstats WebSockets api server
		"WS_SECRET"       : "", // WebSockets api server secret used for login
	}
```

### Run

Run it using pm2:

```bash
cd ~/bin
pm2 start processes.json
```

trustmachine (entrust or gotrust) must be running with rpc enabled.

```
gotrust --rpc
```
the default port (if one is not specified) for rpc under gotrust is 8545

### Updating
To update the API client use the following command:

```bash
~/bin/www/bin/update.sh
```

It will stop the current netstats client processes, automatically detect your trustmachine implementation and version, update it to the latest develop build, update netstats client and reload the processes.