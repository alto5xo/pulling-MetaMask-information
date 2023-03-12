### pulling-MetaMask-information
First of all, you need to create a local server in order to use the MetaMask system.
```js
// Import the Express.js library
const express = require("express");

// Import the built-in Node.js `path` module
const path = require("path");

// Create an instance of the Express.js application
const app = express();

// Set up a route for the root URL (`"/"`) of the application
app.get("/", (req, res) => {
    // Send the HTML file located at the absolute path specified in the `path.join` method
    res.sendFile(path.join(__dirname + "/index.html"));
})

// Start the application on port 5000 and assign the returned `http.Server` object to `server`
const server = app.listen(5000);

// Retrieve the port number on which the application is listening
const portNumber = server.address().port;

// Log a message to the console indicating that the server is running and listening on the specified port
console.log(`port is open on ${portNumber}`);
```

Well, let's move on to ***index.html***.

```html
<!DOCTYPE html>
<html>
    <head>
    <meta charset="UTF-8">
        
<!-- Script tag that imports the @metamask/detect-provider library, which is used to detect the presence of the MetaMask browser extension. -->
<script src="https://cdn.jsdelivr.net/npm/@metamask/detect-provider"></script>
        
    </head>
    <body>
        
<!-- This button element creates a button that, when clicked, triggers the connect() function. -->
<button onclick="connect()">Connect to MetaMask</button> 
        
<div id="account-id"></div>	
<script>
  async function connect() {
    
// If it is positive, it means that the MetaMask extension is installed.
    if (window.ethereum) {
      try {
    
// These lines use the window.ethereum.request() method to retrieve the user's Ethereum account ID. The await keyword is used to wait for the result of the request before continuing. The accountsETH variable contains an array of account IDs, and the accountETH variable is set to the first account ID in the array.
        const accountsETH = await window.ethereum.request({ method: 'eth_accounts' });
        const accountETH = accountsETH[0];
    
// This line sets the innerHTML property of the account-id div element to the user's Ethereum account ID.
        document.getElementById("account-id").innerHTML = accountETH;
    
      } catch (error) {
        console.error(error);
      }
    } else {
    alert('Please make sure MetaMask is installed in your browser.');
    }
}
    </script>
    </body>
</html>
```

#### In case of any error, make sure that MetaMask supports your browser / MetaMask plugin is installed in your browser and the server is running.
