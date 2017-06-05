---
name: Gotrust DAPP Loading Proposal
category: 
---

To have a simple way to load and start Dapps vinay and I came up with a great idea:

1. Dapp packages can be downloaded as .zip/.rlp/.dapp
    - they will contain a `dapp.json` with author info and a dapp name and version.
    - and a `swarm.json`, with all the file paths and hashes, [see here](https://github.com/ThePleasurable/go-trustmachine/wiki/URL-Scheme#server-config-examples))

2. run `$ gotrust install mydapp.zip`, which will verify, extract and copy the dapp locally somewhere.  
**Note** This could also get a name reg domain and looks up the hash an content online, fetches it and installs it.

3. run `$ gotrust start mydapp` will start a node, with the correct options (rpc, corsdomain etc) and start a local server which points with its root into the dapps folder and resolves path and files through the `swarm.json`

4. goto `http://localhost:5555` to see you dapp running (needs to be thought of, as dapps would share localstorage, maybe use a different and reusable port per dapp)

## Update 

- run `$ gotrust update mydapp.zip`, which will extract, and overwrites the old dapp files

## Bundle dapp

- run `$ gotrust bundle myDappFolder/dist/`, which will create a dapp bundle from a folder, to share with others.

- run `$ gotrust deploy myDappFolder/dist/` could save it to pastebin and register it in namereg.