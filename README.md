# Authenti-Kator-2.0, fabric-firebase-logger, and productAuth 

## Table of Contents

- [Overview](#overview)
- [Authenti-Kator-2.0](#authenti-kator-20)
- [fabric-firebase-logger](#fabric-firebase-logger)
- [productAuth](#productauth)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [License](#license)

## Overview
This repository contains three inter-related applications namely Authenti-Kator-2.0, fabric-firebase-logger, and productAuth, aimed at providing authentication and logging services for products. 

## Authenti-Kator-2.0
Authenti-Kator-2.0 is an Android application that allows users to scan QR codes and authenticate the products. The application offers login and signup functionality which are implemented using Firebase DB for storing user credentials.

## fabric-firebase-logger
fabric-firebase-logger is an application that listens for changes in the Firebase DB, particularly the change in product status (isAuthenticated). The DB structure is as follows:

```json
"product_1": {
    "isAuthenticated": false,
    "product_type": "sneakers",
    "serial_number": 116708,
    "authenticated_by": null,
    "authenticated_at": null
}
```

Whenever there is a change detected in the DB, it triggers the `createProduct` method in the chain code.

## productAuth
productAuth is a logging system designed to log the changes of DB in the Hyperledger Fabric. It utilizes chain code to track and log these changes into the Hyperledger Explorer.

## Getting Started

# Getting Started

Follow the instructions below to set up the prodAuth environment and listener app.

## Setting Up the prodAuth Environment

1. Create a `bootstrap.sh` file and put the following code into it:

```bash
#!/bin/bash

echo "Bootstraping..."
minifab netup -s couchdb -e true -o manufacturer.auth.com
sleep 10
echo "Channel Creation..."
minifab create -c authchannel
sleep 10
echo "Channel Joining"
minifab join -c authchannel
sleep 10
echo "Anchor Update"
minifab anchorupdate
sleep 10
echo "Profile Creation..."
minifab profilegen -c authchannel
```

2. Install your chaincode:

```bash
./minifab install -n your_chaincode_name -v 1.0 -l node -p ./chaincode/your_chaincode_name
```

3. Approve, commit, and initialize your chaincode:

```bash
./minifab approve,commit,initialize -n your_chaincode_name -v 1.0 -l node -p ./chaincode/your_chaincode_name
```

4. Invoke a function from your chaincode:

```bash
./minifab invoke -n your_chaincode_name -t your_function_name -p '[arg1,arg2,arg3]'
```

## Setting Up the Listener App

1. Create the fabric-firebase-logger directory:

```bash
mkdir fabric-firebase-logger
cd fabric-firebase-logger
```

2. Initialize the npm project and install the necessary dependencies:

```bash
npm init -y
npm install --save firebase-admin fabric-network
```

Your project directory should look like this:

```plaintext
fabric-firebase-logger
├── node_modules
├── package.json
└── app.js
```

3. Start the app:

```bash
node app.js
```


## Contributing
Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated. Here are the steps to contribute:

1. Fork the project.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.
