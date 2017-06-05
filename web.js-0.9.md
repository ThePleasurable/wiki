---
name: Web.js 0.9
category: 
---

Web3.js 0.9 changes

I would like to apply KISS principle to web3.js. I used the library recently much more and I realised that we are doing to many things implicitly. eg:

1,  newFilter it should either get all logs or poll for new logs. It's shouldn't do both in the same time. In my story, I don't want to poll for filter changes, but I want to get all logs between block X and Y. Same as caktux here: https://github.com/ThePleasurable/web3.js/issues/250

  examples of new solution

  1st.

  ```
var x = web3.entrust.filter(...);		// sync: entrust_newFilter
x.watch(function (err, log) {		// async poll: entrust_getFilterChanges
	
})
  ```


  2nd.


  ```
web3.entrust.filter(..., function (err, x) { 	// async: entrust_newFilter 
	x.watch(function (err, log) { 			// async poll: entrust_getFilterChanges

	})											
}) 	

  ```

  3rd.


  ```
var x = web3.entrust.filter(...)        		// sync: entrust_newFilter
var logs = x.logs();						// sync: entrust_getFilterLogs
  ```

  4th.
  ```
var x = web3.entrust.filter(...)        		// sync: entrust_newFilter
var logs = x.logs(function (err, logs) {	// sync: entrust_getFilterLogs

}
  ```
