# AWS NodeJS

- Preparation: **1 minute**
- Requirements:
  - Initiated Syncano project
  - config with [aws-config](/solutions/aws-config)
- Sockets:
  - [aws-node](https://syncano.io/#/sockets/aws-node)

## Pre installation
If you haven't done that already please [configure](/solutions/aws-config) your syncano instance

## Installing dependencies

To install `aws-node` type:
```sh
$ syncano-cli add aws-node
$ syncano-cli deploy
```

## Done!

Call the create-ls-instance endpoint
```sh
$ syncano-cli call aws-node/create-ls-instance
```

## Testing functionality

Now you can login to your nodejs instance and start creating your fabulous nodejs service.
