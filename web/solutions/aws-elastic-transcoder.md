# AWS Elastic Transcoder Socket

- Preparation: **10 minutes**
- Requirements:
  - Initiated Syncano project
  - AWS config parameters (AWS region, AWS secret access key and AWS access key id)
- Sockets:
  - [aws-elastic-transcoder](https://syncano.io/#/sockets/aws-elastic-transcoder)

### Problem to solve

You want to convert (or “transcode”) media files from their source format into versions that will playback on devices like smartphones, tablets and PCs

### Solution

Our solution is to use [aws-elastic-transcoder](https://syncano.io/#/sockets/aws-elastic-transcoder) to perform the media transcoding in the cloud.

### Setup

#### Installing server dependencies

To install `aws-elastic-transcoder` type:
```sh
$ syncano-cli add aws-elastic-transcoder
```

During installation you will be prompted to provide

**_AWS_REGION_**: The region on which your instance will operate

**_AWS_SECRET_ACCESS_KEY_**: The region on which your instance will operate

**_AWS_ACCESS_KEY_ID_**: The region on which your instance will operate

Proceed to deploy `aws-elastic-transcoder` socket:
```sh
$ syncano-cli deploy aws-elastic-transcoder
```

### Actions to transcode media files

#### Create a pipeline
Create a pipeline that will be used in creating a job for transcoding media files. To create a pipeline send a request to `aws-elastic-transcoder/create-pipeline`

**Required parameters:**

`Name=[string]` - pipeline name

`InputBucket=[string]` - S3 bucket that contains file(s) to transcode

`OutputBucket=[string]` - S3 bucket in which you want Elastic Transcoder to save the transcoded files

`Role=[string]` - IAM ARN role that you want Elastic Transcoder to use to create the pipeline

_Sample input below_

```javascript
const args = {  
   Name:"pipelinePlay",
   InputBucket:"InputBucket",
   OutputBucket:"OutputBucket",
   Role:"arn:aws:iam::293541453747:role/Elastic_Transcoder_Default_Role"
}
```

_Example backend code_

```javascript
import Server from 'syncano-server';

export default async ctx => {
  const { response, socket } = Server(ctx)
  try {
    const pipeline = await socket.post('aws-elastic-transcoder/create-pipeline', ctx.args)
    return response.json(pipeline)
  } catch (err) {
    return response.json(err, 400)
  }
}
```

#### Create a job
Create a job to carry out the transcoding of media files. Send a request to `aws-elastic-transcoder/create-job`

**Required parameters:**

`Inputs=[array]` - Information like bucket key name of the files that you want to transcode

`Outputs=[array]` - Information about the output files(converted files from Inputs media files)

`PipelineId=[string]` - Pipeline to use for transcoding

_Sample input below_

```javascript
const args = {  
   Inputs:[
     {
      Key: "vid2.mp4"
     }
   ],
   Outputs: [
     {
       Key: "vid2_preset1.mp4",
       PresetId: "1351620000001-000010"
     },
     {
       Key: "vid2_preset2.mp4",
       PresetId: "1351620000001-000050"
     }
   ],
   PipelineId: "1511964149448-utee89"
}
```

_Example backend code_

```javascript
import Server from 'syncano-server';

export default async ctx => {
  const { response, socket } = Server(ctx)
  try {
    const job = await socket.post('aws-elastic-transcoder/create-job', ctx.args)
    return response.json(job)
  } catch (err) {
    return response.json(err, 400)
  }
}
```

#### Read a job
Read a job to know the status and other detailed information about a job created. Send a request to `aws-elastic-transcoder/read-job`

**Required parameters:**

`Id=[string]` - The identifier of the job for which you want to get detailed information

_Sample input below_

```javascript
const args = {  
   Id: "1511964149448"
}
```

_Example backend code_

```javascript
import Server from 'syncano-server';

export default async ctx => {
  const { response, socket } = Server(ctx)
  try {
    const jobInfo = await socket.post('aws-elastic-transcoder/read-job', ctx.args)
    return response.json(jobInfo)
  } catch (err) {
    return response.json(err, 400)
  }
}
```