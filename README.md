# Deployment assistant
[![Build Status](https://travis-ci.org/worksolutions/deployment-assistant.svg?branch=master)](https://travis-ci.org/worksolutions/deployment-assistant)

[Russian](README.ru.md)

Assistant safe deployment on production server.

## Goal

Provide a secure deployment process for new Company's developers. 
Eliminate situations in which the production server is in crash status 
due to conflicts during the deployment of the next release.

### A list of possible cases that the assistant can handle

#### There are uncommitted changes on the production server

In this case, the developer will receive a deployment error message:

    Work dir is not clean. Please commit changes

The developer must commit the changes on the production server, 
push them to the remote repository and retry the deployment

#### Remote repository and production server have changes

In this case, the developer will receive a deployment error message:

    The local branch and remote branch are both modified.
    There is risk of conflicts while deploying. 
    
    Please push production changes to remote branch with force parameter, then pull changes locally, 
    then resolve conflicts and try to deploy again.

This situation can cause conflicts. Resolution:

- Make sure that the developer has the latest version of the changes 
on the local computer that he wants to deploy on the production server.
- Push the changes to the remote repository with the -f (force) flag wiping the developer's changes in the repository
- Accept changes from the production server locally and resolve conflicts if they appeared
- Push changes from the local computer to the remote repository
- Try to deploy again 
 
 
#### Changes from the production server are not pushed to the remote repository

In this case, the developer will receive a deployment error message:

    Your local branch is ahead of remote branch. Please push your changes to remote

The developer must push the changes from the production server to 
the remote repository and try to deploy again

#### There are nothing for deployment

In this case, the developer will receive a deployment error message:

    There are nothing to pull

The developer must push the changes from the local computer 
to the remote repository and try to deploy again

## Install

Assistant is an executable phar-archive.
To install, enter the command:

```bash
php -r "copy('http://dep.worksolutions.ru/dep.phar', 'dep.phar');"
chmod +x ./dep.phar
```

Assistant phar-archive is downloaded and saved in your current directory.

Assistant supports php versions from 5.3 to 7.1

## Usage

### Deploy

Deployment command will check the state of the production and remote branches.
After a successful check, you will receive the changes from the remote branch to the production.


Syntax for the deployment command is:

```bash
php ./dep.phar deploy [<remote>] [<branch>]
```

To start deploy, type:

```bash
php ./dep.phar deploy
```

By default, changes will pull from the remote branch `origin/master`, 
to change it is required to specify from which branch of the remote source 
you need to pull the changes:

```bash
php ./dep.phar deploy origin master
```

### Update

Update command will check if there is a new version of the helper and, 
if there is one, will update it.

```bash
php ./dep.phar self-update
```

## Contributing

To make a contribution to the assistant - send pool-requests.
