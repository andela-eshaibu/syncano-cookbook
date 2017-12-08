# AWS S3 Wordpress

- Preparation: **1 minute**
- Requirements:
  - Initiated Syncano project
  - config with [aws-config](/solutions/aws-config)
- Sockets:
  - [aws-wordpress](https://syncano.io/#/sockets/aws-wordpress)

## Pre installation
If you haven't done that already please [configure](/solutions/aws-config) your syncano instance

## Installing dependencies

To install `aws-wordpress` type:
```sh
$ syncano-cli add aws-wordpress
$ syncano-cli deploy
```

## Done!

Call the create-ls-instance endpoint
```sh
$ syncano-cli call aws-wordpress/create-ls-instance
```

## Testing functionality

Now you can login to your wordpress instance and start creating your fabulous wordpress service.
