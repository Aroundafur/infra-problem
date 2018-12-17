# DevOps Assessment

This project contains three services:

* `quotes` which serves a random quote from `quotes/resources/quotes.json`
* `newsfeed` which aggregates several RSS feeds together
* `front-end` which calls the two previous services and displays the results.

## Prerequisites

* Java
* [Leiningen](http://leiningen.org/) (can be installed using `brew install leiningen`)

## Running tests

You can run the tests of all apps by using `make test`

## Building

First you need to ensure that the common libraries are installed: run `make libs` to install them to your local `~/.m2` repository. This will allow you to build the JARs.

To build all the JARs and generate the static tarball, run the `make clean all` command from this directory. The JARs and tarball will appear in the `build/` directory.

### Static assets

`cd` to `front-end/public` and run `./serve.py` (you need Python3 installed). This will serve the assets on port 8000.

## Running

All the apps take environment variables to configure them and expose the URL `/ping` which will just return a 200 response that you can use with e.g. a load balancer to check if the app is running.

### Front-end app

`java -jar front-end.jar`

*Environment variables*:

* `APP_PORT`: The port on which to run the app
* `STATIC_URL`: The URL on which to find the static assets
* `QUOTE_SERVICE_URL`: The URL on which to find the quote service
* `NEWSFEED_SERVICE_URL`: The URL on which to find the newsfeed service
* `NEWSFEED_SERVICE_TOKEN`: The authentication token that allows the app to talk to the newsfeed service. This should be treated as an application secret. The value should be: `T1&eWbYXNWG1w1^YGKDPxAWJ@^et^&kX`

### Quote service

`java -jar quotes.jar`

*Environment variables*

* `APP_PORT`: The port on which to run the app

### Newsfeed service

`java -jar newsfeed.jar`

*Environment variables*

* `APP_PORT`: The port on which to run the app

*Prerequisites*


Here are the prerequisites for this solution:

* AWS Account: Follow these instructions to create an AWS Account: Creating an AWS Account.
* EC2 Key Pair: Follow these instructions to create an EC2 Key Pair: Creating Your Key Pair Using Amazon EC2.
please setup your key pair in the ec2-parameters.json

*Architecture and Implementation*
* CloudFormation: All of the resource generation of this solution is described in CloudFormation  which is a declarative code language that can be written in JSON or YAML.

* Ansible: Within the provisioned instance run Ansible tasks

*Running the solution*
* run bash script cf-deploy.sh
* go to cloudformation, in us-east-1, review the stack that was created. 
* in the output you'll find the instance public ip.

*Next steps*
Continoues integration either via aws' suite:
* CodeCommit: With the addition of the AWS::CodeCommit::Repository resource, you can define your CodeCommit Git repositories in CloudFormation.
* CodeDeploy: CodeDeploy automates the deployment to the EC2 instance that was provisioned by the nested stack.
* CodePipeline: Define CodePipeline’s stages and actions in CloudFormation code which includes using CodeCommit as a Source action and CodeDeploy for a Deploy action (For more information, see Action Structure Requirements in AWS CodePipeline).

Or via one of the popular CI/CD tools like Jenkins.
