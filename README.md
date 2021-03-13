# QCE-Architecure-Pattern-POC
Repository to jot down thoughts, learnings on building an architecure pattern based on CQRS and Event driven architecutre

Query Command Event architecture (QCE) is in similar lines to Model View Controller (MVC) architecture pattern focussed on developing Loosely coupled Microservices. QCE is based on CQRS pattern and Event Oriented Architecure. Unlike CQRS, this pattern will not mandate the use of different models for update and to read data and leaves this upto the architect. This favours RPC over REST Architecture and is closer to GraphQL. QCE can be used to build microservices and run them behind a GraphQL Service or a Gateway API. 

To build a real world application services needs to perform three different operations.  

a. Read the state / data
b. Modify the state 
c. React to events or state modifications happened

**Read the state**
This forms the query part. This will always be a Synchronous Operation and can have async code but the client expects the data to be returned. This kind of service is usedful for fetching data based on id, return search results based on search parameters with sorting on columns etc.

**Modify the state**
This forms the command part. The command will contain the name of the command and payload. The command handler services will perform the required validation and state transition. Once the validation part is success the response can be sent to user while the actual transition can happen asynchronously.

**React to Events**
This forms the Events part. Once a command changes are committed successfully, an Event has occured in the system. We can have numerous event handler services which respond to the event by firing further commands.

Mediation among the services can happen via message broker or mediator framework.

Some outstanding questions?
1. How do we handle concurrent updates? Command from two different systems are resulting in merge conflict? 
2. Should validation and state transition services be separated with validation being synchrounous and state transition services being asynchronous?
3. How do we handle transition failure in command services? May be Handle it as an event and then fire compensation commands.
4. What conventions and standardization can be brought into architecure? like error responses, automatic firing of events, scaffolding of endpoints?
