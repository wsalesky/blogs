# GitHub API XQuery Library
The GitHub API XQuery Library provides XQuery functions for intereacting with the GitHub API (version 3.0). This library currently supports the following functions: create a new branch, commit files to a branch, submit a pull request. 

## Requirements
* EXPath Cryptographic Module Implementation [http://expath.org/ns/crypto]

## Installation
The package can be installed via the eXist-db package manager. 

## Available Functions

Create a new branch:

``` githubxq:branch($base as xs:string?, 
    $branch as xs:string, 
    $repo as xs:string, 
    $authorization-token as xs:string)```

Parameters:
 * $base - The branch to use as base to create new branch from, if empty use master
 * $branch - New branch name
 * $repo - Full path to the GitHub repository
 * $authorization-token - Your personal authorization token. (See: GitHub documentation on authorization tokens [https://github.com/blog/1509-personal-api-tokens])
Returns:
 * item()*
 
Send a commit to GitHub. *A single file.
``` githubxq:commit($data as item()*, 
    $path as xs:string*, 
    $serialization as xs:string?,
    $encoding as xs:string?,
    $branch as xs:string?, 
    $commit-message as xs:string?, 
    $repo as xs:string,
    $authorization-token as xs:string) as item()*```

Parameters:
* $data - Object/file to be commited to GitHub.
* $path - Path to file being commited.  Path must be relative to GitHub repository root, should not start with a slash.
* $serialization - *Not sure this is necessary
* $encoding - utf-8|base64
* $branch - Branch to send commit to. If no branch is specified the default is master.
* $commit-message - Commit message.
* $repo - Full path to the GitHub repository
* $authorization-token - Your personal authorization token.
Returns:
 * item()*
 
Create a new pull request.
``` githubxq:pull-request($title as xs:string?, 
    $body as xs:string?, 
    $branch as xs:string?, 
    $base as xs:string, 
    $repo as xs:string, 
    $authorization-token as xs:string)```
    
Parameters:
* $title - Title of the pull request
* $body - Body/message of the pull request
* $branch - Name of the branch where the changes are
* $base - Name of the branch you want the changes pulled into 
* $repo - GitHub repository
* $authorization-token - Your personal authorization token.
:)


Respond to GitHub webhook requests. If $branch paramter is used the webhook will respond to requests from that branch. Otherwise the webhook responds to activity in the master branch.
``` githubxq:execute-webhook($data as item()*, 
    $application-path as xs:string, 
    $repo as xs:string, 
    $branch as xs:string?, 
    $key as xs:string, 
    $rateLimitToken as xs:string?) ```

Parameters:
* $data - Content of webhook POST request 
* $application-path - Path to eXist-db application 
* $repo - Path to GitHub repository
* $branch - GitHub branch to get data from
* $key - Private key for GitHub authentication 
**          https://developer.github.com/webhooks/securing/
* $rateLimitToken -  Git Token used for rate limiting 
**         https://developer.github.com/v3/#rate-limiting
