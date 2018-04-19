
# Nestify-cli

Simple API client for Nestify Infinity platform. Written in bash.

## Installation

Download the script:

    wget https://raw.githubusercontent.com/nestifyinfinity/nestify-cli/master/nestify-cli;
    chmod 700 nestify-cli

Authentication (Recommended method):

Store your API key in environmental variable NESTIFY_CLI_KEY 

    export NESTIFY_CLI_KEY=REPLACE_WITH_YOUR_API_KEY

Authentication (Alternate method):

Open nestify-cli in a text editor and set appropriate API key on line 2. Make sure to leave the - prefix in place while entering your key. 

API keys can be found at https://nestifyinfinity.com/dashboard/settings

## Command structure

Nestify cli uses structure similar to wp-cli to perform tasks on sites and environments.

    nestify-cli <object> <action> <parameters>

> ## Sites
> Each site on Nestify infinity platform comes with dev, test and live environments by default. You can setup additional environments for each branch of the git repository. Non default environments can pull latest changes from dev and submit their commits as pull requests.

## Create a new site

This will setup a new site and its dev, test and live environments:

    nestify-cli site create

## Delete a site

Delete a site and all associated environments permanently

    nestify-cli site delete <sitename>
    nestify-cli site delete site13123

## List sites

List all active sites

    nestify-cli site list
    
> ## Environments
> Environments facilitate teams to collaborate on the coding, testing and deployments. Standard workflow between environments is feature branch > dev > test > live. 
> 
> Environments can also be used to share latest progress with the team and people outside the organization. Each environment has a unique url, git branch and sftp account.

## List environments
List all environments that belong to a site

    nestify-cli env list <sitename>
    nestify-cli env list site13123

## Create a new environment
Creates a new branch on the git repo and deploys it on a new environment

    nestify-cli env create <sitename> <envname>
    nestify-cli env create site13123 frontend

## Delete environment
Deletes specified environment permanently.

    nestify-cli env delete <envname>
    nestify-cli env delete site13123-frontend

## Environment git log
Shows commit history for specified environment.

    nestify-cli env gitlog <envname>
    nestify-cli env gitlog site13123-dev

## Environment git status
Shows recent changes and untracked files on specified environment.

    nestify-cli env gitstatus <envname>
    nestify-cli env gitstatus site13123-dev

##  Environment git commit
Commits recent changes to git repo's appropriate branch with specified message.

    nestify-cli env gitcommit <envname> "<commit message>"
    nestify-cli env gitcommit site13123-dev "Enabled redis-cache"

## Environment code progress
Shows a list of commits that can be merged from master and commits that can be sent to master for specified environment

    nestify-cli env codeprogress <envname>
    nestify-cli env codeprogress site13123-dev

## Environment composer install
Runs composer install command on specified environment

    nestify-cli env composerinstall <envname>
    nestify-cli env composerinstall site13123-dev

## Environment composer update
Runs composer update command on specified environment

    nestify-cli env composerupdate <envname>
    nestify-cli env composerupdate site13123-dev

## Environment merge commits from master
Merges commits from master into specified environment's git branch

    nestify-cli env mergefrommaster <envname>
    nestify-cli env mergefrommaster site13123-frontend


## Environment merge commits to master
Merges commits from specified environment's git branch into master

    nestify-cli env mergetomaster <envname>
    nestify-cli env mergetomaster site13123-frontend

> ## Deployments
> When commits from dev environment are ready for testing, they are deployed to test environment. Commits need to be deployed to test environment before they can be deployed live. 
>
>Deployments are identified using commit hash and can be rolled back if needed.
> 
## Deploy commits to test environment
Deploy latest commits from dev environment to test environment

    nestify-cli site deploytotest <sitename> <message>
    nestify-cli site deploytotest site13123 "New theme"

## Deploy commits to live environment
Deploy latest commits from test environment to live environment

    nestify-cli site deploytolive <sitename> <message>
    nestify-cli site deploytolive site13123 "New theme"
    
## Review deployment log
Shows log of deployments for specified environment. (Only applicable to test and live)

    nestify-cli env deploylog <envname>
    nestify-cli env deploylog site13123-test
    
## Rollback to a previous deployment
Rollback to a previous deployment using commit hash. (Only applicable to test and live)

    nestify-cli env rollback <envname> <hash>
    nestify-cli env rollback site13123-test 12ea4ce
       
## Import database from another environment
Imports database from another environment to specified environment

    nestify-cli importdb <from envname> <to envname>
    nestify-cli importdb site13123-live site13123-test
    
## Import files from another environment
Imports upload files from another environment to specified environment

    nestify-cli importfiles <from envname> <to envname>
    nestify-cli importfiles site13123-live site13123-test
