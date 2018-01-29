# AWS Comprehend Socket

- Preparation: **8 minutes**
- Requirements:
  - Initiated Syncano project
  - AWS config parameters (AWS region, AWS secret access key and AWS access key id)
- Sockets:
  - [aws-comprehend](https://syncano.io/#/sockets/aws-comprehend)

### Problem to solve

From a document or batch of text documents, you want to determine the dominant language language, extracts key phrases, places, people, brands, or events; understands how positive or negative the text is; and automatically organizes a collection of text files by topic.

### Solution

Our solution is to use [aws-comprehend](https://syncano.io/#/sockets/aws-comprehend) to get all required information.

### Setup

#### Installing server dependencies

To install `aws-comprehend` type:
```sh
$ syncano-cli add aws-comprehend
```

During installation you will be prompted to provide

**_AWS_REGION_**: The region on which your instance will operate

**_AWS_SECRET_ACCESS_KEY_**: The region on which your instance will operate

**_AWS_ACCESS_KEY_ID_**: The region on which your instance will operate

Proceed to deploy `aws-comprehend` socket:
```sh
$ syncano-cli deploy aws-comprehend
```

#### JavaScript client setup
Install

```sh
$ npm install syncano-client --save
```
or

```HTML
<script src="https://unpkg.com/syncano-client"></script>
```

Basic connection

```javascript
const s = new SyncanoClient('YOUR-INSTANCE-NAME');
```

### Actions for aws comprehend socket

#### Sentiment of document
To get the overall sentiment of a document (Positive, Negative, Neutral, or Mixed) send a request to `aws-comprehend/detect-sentiment` endpoint with sample parameter below

```javascript
const param = {
  Text: "Syncano helps the startups in our Fintech and Insurtech accelerator programs to reach product market fit faster",
  LanguageCode: "en"
}
```

*_Using syncano-client library_*

```javascript
s.post('aws-comprehend/detect-sentiment', param)
  .then((res) => {
    console.log(res);
  })
```

*_Using HTTP clients_*
```
  https://<your_instance_name>.syncano.space/aws-comprehend/detect-sentiment/
```

#### Detect key phrases
To detect key phrases and a confidence score to support that this is a key phrase send a request to `aws-comprehend/detect-key-phrases` endpoint with sample parameter below

```javascript
const param = {
  Text: "Syncano helps the startups in our Fintech and Insurtech accelerator programs to reach product market fit faster",
  LanguageCode: "en"
}
```

*_Using syncano-client library_*

```javascript
s.post('aws-comprehend/detect-key-phrases', param)
  .then((res) => {
    console.log(res);
  })
```

*_Using HTTP clients_*
```
  https://<your_instance_name>.syncano.space/aws-comprehend/detect-key-phrases/
```


#### Detect dominant language
To determine the dominant language of the input text for a batch of documents send a request to `aws-comprehend/batch-detect-dominant-language` endpoint with sample parameter below

```
TextList:[
      "Syncano helps the startups in our Fintech and Insurtech accelerator programs to reach product market fit faster",
      "Albert Einstein (14 March 1879 – 18 April 1955) was a German-born theoretical physicist. Einstein developed the theory of relativity, one of the two pillars of modern physics (alongside quantum mechanics)"
    ]
```

*_Using syncano-client library_*

```javascript
s.post('aws-comprehend/batch-detect-dominant-language', { TextList })
  .then((res) => {
    console.log(res);
  })
```

*_Using HTTP clients_*
```
  https://<your_instance_name>.syncano.space/aws-comprehend/batch-detect-dominant-language/
```

#### Detect entities
To detect entities like organisation, location for a batch of documents send a request to `aws-comprehend/batch-detect-dominant-language` endpoint with sample parameter below

```javascript
const param = {
  LanguageCode: "en",
  TextList:[
        "Syncano helps the startups in our Fintech and Insurtech accelerator programs to reach product market fit faster",
        "Albert Einstein (14 March 1879 – 18 April 1955) was a German-born theoretical physicist. Einstein developed the theory of relativity, one of the two pillars of modern physics (alongside quantum mechanics)"
      ]
}
```

*_Using syncano-client library_*

```javascript
s.post('aws-comprehend/batch-detect-entities', param)
  .then((res) => {
    console.log(res);
  })
```

*_Using HTTP clients_*
```
  https://<your_instance_name>.syncano.space/aws-comprehend/batch-detect-entities/
```