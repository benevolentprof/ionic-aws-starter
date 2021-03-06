This project is a repaired version of the [Ionic AWS Starter](https://github.com/ionic-team/starters/tree/master/ionic-angular/official/aws), 
which is intended to work with [AWS Mobile Hub](https://aws.amazon.com/mobile/). 

After my fixes, the app runs, though the avatar image on the Account 
page is a bit wonky. When a user does not have an avatar image, 
the AWS Amplify module returns a URL to a file that doesn't exist, 
which leads to a 404 on the console.
Is this correct behaviour? The doesn't seem to be anything on 
[Amplify issues](https://github.com/aws/aws-amplify/issues?utf8=%E2%9C%93&q=label%3AStorage+) 
and I have asked a 
[question on StackOverflow](https://stackoverflow.com/questions/51070118/what-is-returned-by-storage-get-in-aws-amplify-when-the-file-doesnt-exist).


I think I'm going to shuffle over to Firebase now, 
[just like everybody else](https://ionicframework.com/survey/2017#tools).


This app was created using the following command and repaired 
using some, but not all the fixes, from an 
[issue in their github repo](https://github.com/ionic-team/starters/issues/88). 

```bash
ionic start ionic-aws-project aws
```

**Warning**: Don't try to run the project (`ionic serve`) until quite far in the process.


## Installing AWSMobile CLI

```
npm install -g awsmobile-cli
```


## Creating AWS Mobile Hub Project

Init AWSMobile project. Follow the prompts and accept all the defaults.

```bash
awsmobile init

Please tell us about your project:
? Where is your project's source directory:  src
? Where is your project's distribution directory that stores build artifacts:  www
? What is your project's build command:  npm run-script build
? What is your project's start command for local test run:  ionic serve

? What awsmobile project name would you like to use:  ionic-aws-project

Successfully created AWS Mobile Hub project: ...
```


## Configuring AWS Mobile Hub Project

The starter project gives instructions on how to do this from the 
command line, but some have reported bugs with 
[awsmobile](https://github.com/ionic-team/starters/issues/46), 
so here's how to do it in the browser. 

### NoSQL Database

Enable.

Create a custom table named `tasks`. Make it Private. 

Accept `userId` as Partition key.

Add an attribute `taskId` with type string and make it a Sort key
  
Add an attribute `category` with type string.

Add an attribute `description` with type string.

Add an attribute `created` with type number.

Create an index `DateSorted` with userId as Partition key and taskId 
as Sort key.

### User Sign-In

Turn this on and select verification through email.

Set your password requirements.

Set Multi-Factor Authentication if you wish.



### Hosting and Streaming

Turn this on.

### User File Storage

Turn this on.

#### Configuring S3

From the AWS Console, go to S3.

Select the bucket named `<project name>-userfiles-mobilehub-<AWS resource number>`

Go to the Permissions tab. Click on CORS Configuration. Paste the 
following into the editor and save.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>HEAD</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>GET</AllowedMethod>
    <MaxAgeSeconds>3000</MaxAgeSeconds>
    <ExposeHeader>x-amz-server-side-encryption</ExposeHeader>
    <ExposeHeader>x-amz-request-id</ExposeHeader>
    <ExposeHeader>x-amz-id-2</ExposeHeader>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```


### Integrating Changes into App

Go back to the command line for your project.

```bash
awsmobile pull
```

Answer yes, when asked "? sync corresponding contents in backend/ with #current-backend-info/"



### Install dependencies


```bash
npm install
```

The following commands are needed due to breaking changes in 
[aws-amplify](https://github.com/aws/aws-amplify) 0.4.6. 
They may not be needed in the future.

```bash
npm install @types/zen-observable
npm install @types/paho-mqtt
```

### Run the app

```bash
ionic serve
```


There are a couple more instructions on running and hosting in the 
README for the original project.

