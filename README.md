# GitHub API XQuery Library
The GitHub API XQuery Library provides XQuery functions for intereacting with the GitHub API (version 3.0). This library currently supports the following functions: create a new branch, commit files to a branch, submit a pull request. 

## Requirements
* EXPath Cryptographic Module Implementation [http://expath.org/ns/crypto]

## Installation
The package can be installed via the eXist-db package manager. 

## Available Functions
Create a new branch
```githubxq:branch($base as xs:string?, 
    $branch as xs:string, 
    $repo as xs:string, 
    $authorization-token as xs:string)```
