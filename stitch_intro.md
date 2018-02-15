# MongoDB Stitch Introduction
##Drew DiPalma, Product Manager
10:10 

###Goals
    - when building, you need to safety & easily access data
    - integrate with key services
    - scalably serve requests

###MongoDB Stitch
    - Native SDKs (js, android or OS)
    - Rest-like APIs
    - 3rd party services integration
    - functions
    - integrated results
    - mongoDB query language + native drivers
    - MongoDB Atlas
    - stitch sits @ direct DB access
    - above: integrated services & functions for coplex, connection logic
    - below: Native SDKs
    - when request coming from client: 
        1. app request made
        2. Stitch parses & applies rules
        3. Stitch orchestrates DB + services
        4. Stitch aggregates & applies rules
        5. Client receives results

####code provided on how Stitch works, from MongoDB concepts:
    ...
    .then(stitchClient => {
        client = stitchClient;
        mondodb = client.service...
        })
        ....
    - client.login().then(() => {
        ...
        })
    - you can use client.authenticate() to access other auth providers
        client.authenticat('providerType', {options})
        ...
    - coll.find ( or any aggregate command)

####from Services concept:
    - const twilioService = client.service...
    - const sesService = client.service...
    - constS3Service = client.service...
    - stitch functions: 
        scalable, hosted JS functions
        written using EmcaScript 5
        easilly incorporate application contect
            context.values
            context.services
            context.user
            .request
            .functions
            .utils
        - great for low latency request client, maybe do ETL from appl to db
        - have yet to optimize for heavy compute work, that's when you'd want to use a serverless app such as lambda, which stitch works with

####from functions concept:
    - client.executeFunction();
    ...
    return statuses;
####declarative access controls
    - control db/service/function access
    - fine grained data access controls
    - define with simple json or link to functions
    - associate with user prfile, MDB data, or external info
####Example: Banking app
    - 3 types of users: 
        1. user, access account
        2. bank teller, access some info
        3. analyst, needs to access info in aggregate but not in specific users/docs
    - would normally:
        - application
        - roles, permissions, security
        - Atlas
    - with stitch, you can do all of this
    - customer makes request to Stitch, stitch to atlas, atlas to stitch
    - stitch checks user auth to see if they can read the data before serving
    - bank teller: makes request to stitch, goes to atlas, responds with document, and stitch checks again
    - stitch strips out data that bank teller cant see
    - analyst: cannot access anything but aggregate data. but can create special function for them, to grab aggregation info, return aggregated data

####Stitch in Action
    - 2FA access control w/ stitch
    - ....

####Ways to use Stitch
    - add features
        - take app to new platform
        - bld better permissions or separate admin profile
        - add add'l auth providers
        ...
    - expose data
        - provide API for safe int data access
        ...
    - integrate services
    - complete backend

####Pricing
    - $1/GB data transferred from Stitch to client/service
    - 25GB free data/month
    - data transfer to Atlas free

####What's coming next
    - stitch still in beta
    - improve dev
        - app import/export tools
        - user/log management rules usability
    - realtime
        - change streams drive event-based pipelines
    - everywhere
        - expand regional footprint 
        - avail. on-premise 
        - bring any MongoDB
####Next
    - hand on lab
    - stitch.mongodb.com
    - check out SDKs & examples
        - code @ github.com/mongodbstitch
        - docs.mongodb.com/stitch
        - build dashboard or weather IoT apps

