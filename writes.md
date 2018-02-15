#It's 10 pm, do you know where your writes are?
    Shane Harvey, software engineer, MongoDB
###MongoDB 3.4 Scenario
    - running update, get network error
    - no way to retrieve operations state
    - retry strategies: 

                |transient network error|persistent outage
    never retry |may undercount         |ok
    always retry|may overcount          |wastes time
    retry once  |may overcount          |ok
    - no good solution for transient network errors
    - why can't we retry, find out if it succeeded on network or not
    - state tied to connecton objects; once conn. object dies, all state is lost
###MongoDB 3.6
    - MongoDB 3.6 introduces logical sessions, allow us to maintain cluster-wide state about user & their operations
    - sessions not tied to connections

###Retryable Writes
    - send session id with update to server, gets lost, server remembers ID and that it was performed, can retry for you, update should success. 
    - won't reapply update if already occured
    - if never exe., do it now, return result
    - sessions are cluster-wide
    - To enable:
      mongodb://...?retryWrites=true

###Zombie Cursor Cleanup
    - running long query: cursor.forEach(function() {
        // lengthy processing...
    });
    - error: cursor doesn't exist anymore after 10 min, closes
    - issuing a getMore will reset internal clock
    - for long operation, disable cursor: noCursorTimeout: true
    - exe. long query, then network fails
        - hours later, do you know where your cursors are? 
        - zombie cursor; stuck on server, holds resources
        db.serverStatus()
        {
            ...
        }
    - logical sessions, also has a timeout

###Cluster-wide killop
    - db.currentOp()
    {
        "inprog" : [

        ]
    }
    db.killOp(132921);
    but you have to do that for every server running this query
    - logical sessions: cluster-wide killOp with logical sessions
    - any operation may be killed
    - send killSessions command to db

    - no need to rewrite apps
    - opting in to retryable writes
    - new API for client session
    - mongodb/specifications: /sessions, /retryable-writes, /casual-consistency
    - expect more from sessions in the future
    - rest easy
    