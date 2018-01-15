## AWS Configuration

- Preparation: **2 minutes**
- Requirements:
  - Initiated Syncano project
  - AWS ACCOUNT_KEY
  - AWS SECRET
- Sockets:
  - [aws-config](https://syncano.io/#/sockets/aws-config)

## Base 
This socket is base socket for  all the aws sockets.

## Installing dependencies

To install `aws-config` type:
```sh
$ syncano-cli add aws-config
$ syncano-cli deploy
```

Now you have to provide ACCOUNT_KEY and SECRET key for the AWS Service:
```sh
$ syncano-cli call aws-config/install
```

#### AWS_ACCESS_KEY_ID 
that's an access key to your aws account.

#### AWS_SECRET_ACCESS_KEY 
that's a secret key to your aws account.

#### REGION 
That's a region on which your instance will operate.

Our solution is based on [aws-storage](https://syncano.io/#/sockets/aws-storage) Socket will be used to communicate with S3 and make it super easy to use this service.