# Rest Framework

- Preparation: **3 minutes**
- Requirements:
  - Initiated Syncano project
- Sockets:
  - [rest-framework](https://syncano.io/#/sockets/rest-framework)

## Solution

This framework should be used for general CRUD purposes. It entangles the complicated permissions flow with one simple tool so you dont have to code backend for your syncano classes.

## Installing dependencies

Install rest-framework and rest-auth for authorization

```sh
$ syncano-cli add rest-framework rest-auth
$ syncano-cli deploy
```

Provide an email for adminstrator user, you will be asked for.
Provide your superuser key.
Now you are ready to use it with our frontend admin
[react-syncano](https://github.com/Aexol/react-syncano)

If you want to use it without our frontend package, you have to call
the configure endpoint yourself either being logged in as administrator user or providing REST_FRAMEWORK_KEY in call args. You can also call it using syncano-cli

```sh
$ syncano-cli call rest-framework/configure
```

## Done!

Now you can use the rest framework
