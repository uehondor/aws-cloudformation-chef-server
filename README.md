Setup Chef Server on AWS EC2 using CloudFormation
=================================================

If you've ever tried to setup Chef Server on AWS with CloudFormation (CF) using the official template ([found here]( https://s3.amazonaws.com/cloudformation-templates-us-east-1/chef-server-ubuntu-configuration.template)), you'll understand when I say it isn't a stroll in the park.

I hope to make it a little easier to setup Chef Server on EC2 by creating a CF template that works and is (somewhat) easy to read and follow.

The secret weapon here is an up-to-date version of the [`Chef Server Cookbook`](https://github.com/opscode-cookbooks/chef-server).


### How to use
Using the template to setup a Chef Server should be pretty straight-forward.

Here's an example using [`awscli`](http://docs.aws.amazon.com/cli/latest/index.html) command line tool:
```
aws cloudformation create-stack --stack-name "chef-server" --template-body file:///path/to/aws-cf-chef-server.json --capabilities ... --parameters ...
```

######Note:

AWS Resources: This will create an EC2 instance (m1.small) and S3 bucket.

Parameters: The the template expects four parameters: `ChefServerCookbookVersion`, `InstanceType`, `KeyName`, `ChefServerFQDN` and `SSHLocation`. These are self-explanatory. `KeyName` and `ChefServerFQDN` are required.

Access Keys: The .pem keys needed by [`knife`](http://docs.opscode.com/knife.html) to access the chef server from your workstation will be copied to the S3 bucket. You can download the keys from there.


### Test on Vagrant
If you want to have a play without racking up a few cents/pennies, you can setup chef server on a [`Vagrant`](http://www.vagrantup.com) VM.

All you need to do is `vagrant up --provision`.

Note: You need to have [`vagrant-librarian-chef`](https://github.com/jimmycuadra/vagrant-librarian-chef) plugin installed.
