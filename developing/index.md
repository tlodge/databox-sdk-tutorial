---
layout: base
title: sdk dev wishlist
---

We have not yet got decent docuementation on how to develop the SDK.   The front-end code is written in react/redux, and was an originally a partial port of the node-red code.  To have a play you'll need to have docker and git installed on your machine.  Then do the following:

```javascript
git clone https://github.com/me-box/platform-sdk.git
cd ./platform-sdk/src/server
npm run install
npm run dev
```

This will pull all of the docker containers the sdk is dependent on and start the server.

Now to run the sdk client in dev mode (i.e. open another terminal and move to the platform-sdk/src/client directory and) run:

```javascript
npm install
npm start
```

This will create a dev server (with hot reloading) that serves up the client, and proxies requests to the dev server.
