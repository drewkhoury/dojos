CloudFormation 101
==================

# Objectives

This repository is intended to be a primer on the use of AWS CloudFormation for the automatic creation of AWS resources.

Assumptions: Little to no AWS experience prior to the session.

# About this repository

This repository contains a presentation to guide you through the training, plus all required supporting code.

**Presentaiton**
`./presentation` is a HTML based presentation to guide you through the training session.

**Source**
`./src/setup` contains information about preparing the training session for the first time.
`./src/exercise-*` contains the supporting material, referenced in the presentation.

# Prerequisites

* An AWS account with a user that can execute CloudFormation stacks (along with EC2 & SQS)
* A basic knowledge of JSON
* A ssh public key to ssh to an ec2 instance

# Setup Instructions

** Simple (for one person)**
For the exercises to work you'll need a few basic supporting components (VPC, Subnet, Security Group). AWS provides these by default so you could skip the setup if you're only interested in completing the exercises yourself.

** Advanced (to run your own demos)**
For advanced setup see [Setup](aws-cloudformation-101/src/setup)

# Exercises

The presentation is created in revealjs and intented to be run locally on your computer. Once you've cloned this repo, go to aws-cloudformation-101/presentation/index.html and follow along.
