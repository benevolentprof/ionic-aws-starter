This project is a repaired version of the [Ionic AWS Starter](https://github.com/ionic-team/starters/tree/master/ionic-angular/official/aws) 


It was created using the following `ionic start` and repaired 
using instructions from an [issue in their github repo](https://github.com/ionic-team/starters/issues/88). 

```bash
ionic start myApp aws
```

**Warning**: Don't try to run the project (`ionic serve`) until quite far in the process.


### Installing AWSMobile CLI

```
npm install -g awsmobile-cli
```


### Creating AWS Mobile Hub Project

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


### Configuring AWS Mobile Hub Project

The starter project gives instructions on how to do this from the 
command line, but some have reported bugs with 
[awsmobile](https://github.com/ionic-team/starters/issues/46), 
so here's how to do it in the browser. 

#### NoSQL Database

Enable.

Create a custom table named `tasks`. Make it Private. 

Accept `userId` as Partition key.

Add an attribute `taskId` with type string and make it a Sort key
  
Add an attribute `category` with type string.

Add an attribute `description` with type string.

Add an attribute `created` with type number.

Add an index `DateSorted` with userId as Partition key and taskId as Sort key.

#### User Sign-In

Turn this on and select verification through email.

Set your password requirements.

Set Multi-Factor Authentication if you wish.

#### User File Storage

Turn this on.

#### Hosting and Streaming

Turn this on.


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

The following commands are needed due to breaking changes in [aws-amplify(https://github.com/aws/aws-amplify) 0.4.6. They may not be needed in the future.

```bash
npm install --save-dev @types/zen-observable
npm install --save-dev @types/paho-mqtt
npm install --save-dev @types/node
```

### Run the app

```bash
ionic serve
```




Original README below
----------------------


# Ionic AWS Starter

This Ionic starter comes with a pre-configured [AWS Mobile Hub](https://aws.amazon.com/mobile/) project set up to use Amazon DynamoDB, S3, Pinpoint, and Cognito.

## Using the Starter

### Installing Ionic CLI 3.0

This starter project requires Ionic CLI 3.0, to install, run

```bash
npm install -g ionic@latest
```

Make sure to add `sudo` on Mac and Linux. If you encounter issues installing the Ionic 3 CLI, uninstall the old one using `npm uninstall -g ionic` first.

### Installing AWSMobile CLI

```
npm install -g awsmobile-cli
```

### Creating the Ionic Project

To create a new Ionic project using this AWS Mobile Hub starter, run


Which will create a new app in `./myApp`.

Once the app is created, `cd` into it:

```bash
cd myApp
```

### Creating AWS Mobile Hub Project

Init AWSMobile project 

```bash
awsmobile init

Please tell us about your project:
? Where is your project's source directory:  src
? Where is your project's distribution directory that stores build artifacts:  dist
? What is your project's build command:  npm run-script build
? What is your project's start command for local test run:  ionic serve

? What awsmobile project name would you like to use:  ...

Successfully created AWS Mobile Hub project: ...
```

Enable user-signin and database features

```bash
awsmobile features

? select features:
 ◉ user-signin
 ◉ user-files
 ◯ cloud-api
❯◉ database
 ◉ analytics
 ◉ hosting
```

Configure database, create a table with name `tasks`

```bash
awsmobile database configure

? Select from one of the choices below. Create a new table

Welcome to NoSQL database wizard
You will be asked a series of questions to help determine how to best construct your NoSQL database table.

? Should the data of this table be open or restricted by user? Open
? Table name tasks

 You can now add columns to the table.

? What would you like to name this column taskId
? Choose the data type string
? Would you like to add another column Yes
? What would you like to name this column userId
? Choose the data type string
? Would you like to add another column Yes
? What would you like to name this column category
? Choose the data type string
? Would you like to add another column Yes
? What would you like to name this column description
? Choose the data type string
? Would you like to add another column Yes
? What would you like to name this column created
? Choose the data type number
? Would you like to add another column No

... /* primary and sort key */

? Select primary key userId
? Select sort key taskId

... /* index */

? Add index Yes
? Index name DateSorted
? Select partition key userId
? Select sort key created
? Add index No
Table tasks saved
```

Finally push the changes to server side

```bash
awsmobile push
```

### Running the app

Now the app is configured and wired up to the AWS Mobile Hub and AWS services. To run the app in the browser, run

```bash
ionic serve
```

To run the app on device, first add a platform, and then run it:

```bash
ionic cordova platform add ios
ionic cordova run ios
```

Or open the platform-specific project in the relevant IDE:

```bash
open platforms/ios/MyApp.xcodeproj
```

### Hosting app on Amazon S3

Since your Ionic app is just a web app, it can be hosted as a static website in an Amazon S3 bucket.

```
npm run build
awsmobile publish
```
