## 09:00 2/15/18 Keynote
Susan Palmer, RVP NW introduced
Eliot Horowitz, CTO & Founder

### MongoDB Server 3.6: 
    - #lookup 
    - arrays: update all items with one line:
        // ♥ db.order.update...
        // ♥ "line_items.$[li].price":
        called "fully expressive array updates"
    - schema: always schema ass. with data
        mod. quickly while keeping enforcement of db
        json schema support added, some extension
        $jsonSchema: {....
        }
        put on collection, with all inserts/updates, will make sure that docs inserted are valid. as flexible as designre
        adv chema design patters talk
    - retryable writes
        high availability during failure (< 1.6s)
        db & driver
        network, hardware error; if happens, retry the operation with:
        uri = "mongodb://example.com:27017/?retryWrites=true"
    - change streams: gives feed of all changes happening in db
        update upstream/downstream data is easier
        cursor = client.my_db.my_collection.watch([...])
        for change in cursor:
            print(change['newDocument'])
    - place an order: what happens if there's an error? before or while iterating array? can have background process that updates inventory...painful!
    session.start_transaction()
    ...
    session.commit_transaction()
    therefore:
    multi-document ACID transactions coming in 4.0!

###MongoDB 4.0: single replica set transactions
    - familiar
    - conversational
    - multi-doc, multi-statement
    - snapshot isolation / point-in-line
    - ACID
    - no performance cost for non transaction operations
    - when to use transactions in mongodb? 
    - inserts and updates roll up view in 
    - been working on ACID for 3 yrs
    - 4.2: sharded transactions
    - change streams and retryable writes are in 3.6, these are the bldg blocks for sharded transactions
    - join the beta program: mongodb.com/transactions

###business intelligence: how to get out of mdb and analyze as fast as possible
    - BI connector has been around
    - BI connector 2.0 came out in december
    - polymorphic documents: docs in mongo aren't flat
    - arrays: 2 ways to look at it; find most popular items, or histogram of order of price
    - built with MongoDB charts; native dashboard charts in MongoDB
    - Grigori Melnik giving demo: (head of product, server & tools)
    - mdbw17.stack_overkill demo, &c.

###Atlas 
    Since Launch:
    - free tier
    - live migration service
    - data browser
    - real-time peformance viewer
    - performance advisor
    - M2 tier
    - Atlas BI connector (now built in to Atlas)
    - queryable backups (can query live while on backup data, w/i 2 min or less, look it up and shut it down)
    - pause cluster
    - Atlas avail. on AWS, Azure, Google Cloud
    - main loc. on West coast, and secondary Atlas regions as desired
####Demo: Muthu Chinnasamy, principle solutions architect in Seattle
    - Build Cluster: version (MongoDB 3.4 with WiredTiger), cloud provider, region, instance size (multiple tiers)
    - sandbox, global app, test failover option, alerts, hundreds of metrics, 

####Atlas coming soon
    - Full CRUD support
    - charts integration
    - Auditing
    - LDAP authenticaton
    - KMIP integration (for your own incryption keys)
    - cross cloud clusters (same as cross region clusters today)

### MongoDB Stitch
    - BaaS for MongoDB
    - what's changed since 2007?
        - Web as 1st-class UI
        - Mobile
        - IoT
        - Services. Amazon SES, github, google cloud messaging, &c.
    - a modern app needs an API to do CRUD and security , access control, logic, and validation, and a way to stitch services together
    - today, do this with custom node/python/rails app, boilerplace, DIY security & privacy
    - MBAAS/PAAS/Serverless Way today, but can't get at your data, can't use other services, & you're locked in
    - stitch is different! 
    REST API for MongoDB
    - configuration based authentication, privacy, security
    - service composition
    - anywhere you want
    - (image on stitch arch)
    - BI tools, MongoDB atlas (shell access), stitch to services / mobile

#### Eliot performs demo:
        - Blog, want to add comments
        1. write HTML 
        2. insert boilerplate from stitch into head tag
        3. turn on anonymous login for demo
        4. displayComment():
        5. userId ...
        6.  function displayComments(): {
            db.collection("comments").find({}).execute().then(docs => {
              ...
            }
            function addComment(): {
                ...
            }
        7. webhook with twilio...text comment to phone number, excellent joke inserted (you have to be there)
