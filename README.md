# Akamai Devops World Tour 2018 Trip Report

* Atlanta, GA
* October 23, 2018
* Michael Fyffe

## What is Akamai Devops World Tour 2018

This was a chance to get hands-on training from Akamai's Experts on their devops tools and understand how they fit into a devops process.  
The focus was around Akamai's Devops Initiative and the solutions they currently provide and are working on.
It is also a chance to network with other Akamai Devops Experts from around the globe and understand how they are currently utilizing 
Akamai in the real world today.

## Why I chose to attend Akamai Devops World Tour 2018

I wanted to attend this primarily to better understand how we can transition our manual akamai processes to a more modern configuration-as-code approach.  This would allow us to effectively & more efficently automate our processes.

Since this devops movement is still new and rapidly evolving for akamai I anticipate gaining a better understanding of the maturity level of their tools for consumption in practice.

I _also_ wanted to see how others are implementing these cutting-edge technologies in the enterprise, especially from an automation or management perspective.

## Conference Takeaways

+ Akamai's is taking an open-source approach with a community-focus.
    + Requesting features is as simple as opening a github issue.
    + Contributing is as simple as creating a PR ( of course get some discussion going on an issue before writing code ).
    + Akamai is working on ways to get the community more involved so more to come.
+ New API Gateway
    + Seamless Swagger integration
    + Protects public API's
        + Rate Controls
        + Lock down specific api paths
        + WAF + BOT + DDOS Protection
        + Performs authentication/authorization
            + Reject requests before they reach your origin
    + Ability to perform caching
+ Akamai Offers something called "Live Updates"
    + You want to cache as much as possible but you don't want stale data.  This solves it
    + you can do this via multiple ways
        + Luna portal
        + CLI
        + Rest API
+ World Tour Recap
    + https://developer.akamai.com/akamai-developer-world-tour/recap?utm_source=mkto&utm_medium=email&utm_campaign=ME11513&mkt_tok=eyJpIjoiWW1Rd05UQTBNRFF6WVRNdyIsInQiOiJOd2E5ekNKYkc4citEeU1SeWdMMmY0RDdmTFB0YnZad2piVzFibmcrbnpyU3IyUlkxSFV5SUx1REVFUU8zNnJLY25nZUxJa0VOUVhvbWRVV2k1MkZLMGRFUEJ5V25TemJTYlR0ZkNSV1QzeVF5V2xHRUd4dWR2WUlhMHdKdDBBZiJ9

## Conference Action Items

+ [X] Schedule a day to have a Lunch-N-Learn conference recap.  This is to talk about the conference, what we did, and what we learned.

## Detailed Session Information

### API Gateway

#### Summary

Most applications nowadays are microservices.  This means there are alot of web api's that developers are creating to support their application.  API Gateway is where this can help.  Property manager is not really meant
for API's so this is their solution.

https://developer.akamai.com/api-gateway

+ What we did
    1. Create API Gateway
    1. Import a swagger api definition document ( swagger.json ) so akamai knows about the api operations
    1. Enable api keys and configure it so this key should be found in the http authorization header
    1. Make all api endpoint methods private ( require authentication )
    1. Make a certain endpoint public and not require authentication/authorization
    1. Active the api gateway configuration in the ESN
    1. Create some api key with quotas ( 100 calls in an hour )
        - These allow identifing access
        - Quota Tracking
    1. Define what resources/endpoints certain key collections can utilize
    1. Make an http call with and without the key to see forbidden and OK
    1. Enable Kona Site Defender to protect the origin from harmful payload and requests


#### Takeaways

+ API Gateway replaces property manager for API's.
    + Property Manager is really for websites
+ API Gateway can help with the following:
    1. Authorization
    1. Authentication
    1. Quota Enforcement
    1. Payload Validation
    1. Endpoint Visibility
    1. Protection ( bots etc.. )
+ When you have Authentication and Authorization for an API you cannot just cache this like normal akamai.  Authentication
  And authorization has to happen for every call.  This is where API Gateway comes in and feels the gaps on property manager.
+ If you have many web api's do you really want to duplicate authentication/authorization logic across all these?  This should be centralized
+ Presents a single plane of glass of how your api gateway is doing.
    1. Security
    1. Performance
    1. Centralized Management

#### Action Items

+ [ ] Read up about Akamai's api gateway
+ [ ] Inform everyone that is an option when talking about API Gateways and public API's
+ [ ] Do the akamai trial for api gateway to get a free google home mini
    + http://bit.ly/api-gateway-free-trial
    + https://developer.akamai.com/api-gateway-free-trial-thank-you

### Akamai Pipeline

#### Summary

Akamai pipeline allows you to store your akamai configuration in code.  It templatizes your configuration so that you can reuse and easily setup akamai in all your environments using templates.  It also helps you utilize
the pattern Akamai recommends for setting up akamai in your environments, that is 1 property per environment.

+ What we did
    1. Create a pipeline that has the dev and prod environment
    1. Our properties have multiple origins so we had to declare variables for these and set their environment specific values
    1. We then merged to see the resulting papi json and see validation happen
    1. We then promoted to the development environment
    1. We added an image manager behavior and rules

#### Takeaways

+ Right now companies using Akamai just push to production and hope it works.  It also becomes a situation where they get all the way to production
  and the application is broken.
+ Akamai Pipelines was structured in a way to help with federated development
    + Instead of of 1 giant json rule file it is split up into multiple smaller json files.  This helps with:
        + Less merge conflicts
        + Merge conflicts are easier to resolve if one happens
+ Akamai Pipelines is a fully client side application
    + PAPI has no concept of pipelines as this is solely a concept of Akamai Pipelines application.
    + Because it's full client side you have to keep track of the state of the pipeline and promotions.
        + This requires extra commits after promotions which is not ideal
        + Dealing with remote state is painful.  Hopefully they will integrate a backend later like terraform OR we can
          use terraform to replace this once it becomes more complete.

#### Action Items

+ [X] Pass the "Akamai Developer World Tour Developer Workbook" to my team members so they can walk through creating and promoting in an akamai pipeline.

### Image Manager

#### Summary

Image Manager will automatically optimize images at the edge.  You can create Image manager policies indicating what transformations should happen at the edge.

#### Takeaways

+ An algorithm that obtained an emmy is used to optimize images
    + The optimization can optimize an image that reduces it's size but leaving the human eye unable to see
      a difference in quality.  It's called Image Perception optimization
+ Can automatically scale and resize images so you can use them in multiple places on your application
+ Can automatically crop faces out of images for you.

#### Action Items

+ [ ] Learn and Understand if/how image manager is setup in our akamai configurations.

