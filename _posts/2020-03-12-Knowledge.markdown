---
layout: post
title:  "Jenkins Pipeline, CORS, Polly, RabbitMQ, EasyNetQ, NoSQL, E2E Testing, Unit testing, Itegration tests, Trunk-Based Development, Git Flow vs Github Flow"
date:   2020-03-12 12:46:54 +0200
categories: jekyll update
---
Jenkins Pipeline
-

`Jenkins Pipeline` (or simply "Pipeline" with a capital "P") is a suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins.

A continuous delivery (CD) pipeline is an automated expression of your process for getting software from version control right through to your users and customers. Every change to your software (committed in source control) goes through a complex process on its way to being released. This process involves building the software in a reliable and repeatable manner, as well as progressing the built software (called a "build") through multiple stages of testing and deployment.

Pipeline provides an extensible set of tools for modeling simple-to-complex delivery pipelines "as code" via the Pipeline domain-specific language (DSL) syntax. [1]

The definition of a Jenkins Pipeline is written into a text file (called a Jenkinsfile) which in turn can be committed to a project’s source control repository. [2] This is the foundation of "Pipeline-as-code"; treating the CD pipeline a part of the application to be versioned and reviewed like any other code.

Creating a Jenkinsfile and committing it to source control provides a number of immediate benefits:

Automatically creates a Pipeline build process for all branches and pull requests.

Code review/iteration on the Pipeline (along with the remaining source code).

Audit trail for the Pipeline.

Single source of truth [3] for the Pipeline, which can be viewed and edited by multiple members of the project.

While the syntax for defining a Pipeline, either in the web UI or with a Jenkinsfile is the same, it is generally considered best practice to define the Pipeline in a Jenkinsfile and check that in to source control.

More is here: [link][pl]

---

Cross-origin resource sharing (CORS)
-

`Cross-origin resource sharing (CORS)` is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.

A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos. Certain "cross-domain" requests, notably Ajax requests, are forbidden by default by the same-origin security policy. CORS defines a way in which a browser and server can interact to determine whether it is safe to allow the cross-origin request. It allows for more freedom and functionality than purely same-origin requests, but is more secure than simply allowing all cross-origin requests.

The specification for CORS is included as part of the WHATWG's Fetch Living Standard. This specification describes how CORS is currently implemented in browsers. An earlier specification was published as a W3C Recommendation.

More is here: [link][cors]

---

Polly
-

`Polly` is a .NET resilience and transient-fault-handling library that allows developers to express policies such as Retry, Circuit Breaker, Timeout, Bulkhead Isolation, and Fallback in a fluent and thread-safe manner. Polly targets .NET 4.0, .NET 4.5 and .NET Standard 1.1.

Polly helps you navigate the unreliable network. By providing resilience strategies in fluent-to-express policies such as Retry, WaitAndRetry, and CircuitBreaker, Polly can help you reduce fragility, and keep your systems and customers connected. Example usages are fault-tolerance for any distributed systems and inter-process calls, such as WCF, RESTful calls between microservices, calls to cloud services, Internet of Things (IoT) connectivity, messaging systems, calls to your persistence layer (eg. wrapping Entity Framework), etc.

While there are other frameworks for .NET that include a circuit-breaker, Polly is the only comprehensive resilience framework for in this space. The closest comparison is Netflix's Hystrix project, built on the Java platform. However, we plan on taking Polly beyond what Hystrix provides, but targeted specifically to the .NET framework.

An ambitious roadmap targets policies for bulkhead isolation, timeouts, caching, fallback and load-shedding, preventing catastrophic failure for systems under load. Bulkhead isolation is interesting in that it prevents runaway faults from swamping systems, by grouping operations to isolated resource pools.

Best of all, Polly is a zero-dependency, lightweight library that can work anywhere .NET can run. Whether you’re building an occasionally connected mobile application, or a heavy duty business intelligence service, simply drop in the Polly NuGet package and get started right away!

More is here: [link][pol]

---

RabbitMQ
-

`RabbitMQ` is a message broker: it accepts and forwards messages. You can think about it as a post office: when you put the mail that you want posting in a post box, you can be sure that Mr. or Ms. Mailperson will eventually deliver the mail to your recipient. In this analogy, RabbitMQ is a post box, a post office and a postman.

The major difference between RabbitMQ and the post office is that it doesn't deal with paper, instead it accepts, stores and forwards binary blobs of data ‒ messages.

RabbitMQ, and messaging in general, uses some jargon.

Producing means nothing more than sending. A program that sends messages is a producer:

(P)

A queue is the name for a post box which lives inside RabbitMQ. Although messages flow through RabbitMQ and your applications, they can only be stored inside a queue. A queue is only bound by the host's memory & disk limits, it's essentially a large message buffer. Many producers can send messages that go to one queue, and many consumers can try to receive data from one queue. This is how we represent a queue:

queue_name
[|||||]

Consuming has a similar meaning to receiving. A consumer is a program that mostly waits to receive messages:

(c)

Note that the producer, consumer, and broker do not have to reside on the same host; indeed in most applications they don't. An application can be both a producer and consumer, too.

More is here: [link][rab]

---

EasyNetQ
-

`EasyNetQ` is a simple to use, opinionated, .NET API for RabbitMQ.

The goal of EasyNetQ is to provide a library that makes working with RabbitMQ in .NET as simple as possible. In order to do this, it has to take an opinionated view of how you should use RabbitMQ with .NET. It trades flexibility for simplicity by enforcing some simple conventions. These include:

Messages should be represented by .NET types.
Messages should be routed by their .NET type.
This means that messages are defined by .NET classes. Each distinct message type that you want to send is represented by a class. The class should be public with a default constructor and public read/write properties. You would not normally implement any functionality in a message, but treat it as a simple data container or Data Transfer Object (DTO). Here is a simple message:

{% highlight C# %}
public class MyMessage
{
    public string Text { get; set; }
}
{% highlight %}

EasyNetQ routes messages by their type. When you publish a message, EasyNetQ examines its type and gives it a routing key based on the type name, namespace and assembly. On the consuming side, subscribers subscribe to a type. After subscribing to a type, messages of that type get routed to the subscriber.

By default, EasyNetQ serializes .NET types as JSON using the Newtonsoft.Json library. This has the advantage that messages are human readable, so you can use tools such as the RabbitMQ management application to debug message problems.

More is here: [link][eq]

---

NoSQL
-
`NoSQL` is an approach to database design that can accommodate a wide variety of data models, including key-value, document, columnar and graph formats. NoSQL, which stands for "not only SQL," is an alternative to traditional relational databases in which data is placed in tables and data schema is carefully designed before the database is built. NoSQL databases are especially useful for working with large sets of distributed data.

NoSQL vs. RDBMS

The NoSQL term can be applied to some databases that predated the relational database management system, but it more commonly refers to the databases built in the early 2000s for the purpose of large-scale database clustering in cloud and web applications. In these applications, requirements for performance and scalability outweighed the need for the immediate, rigid data consistency that the RDBMS provided to transactional enterprise applications.

Notably, the NoSQL systems were not required to follow an established relational schema. Large-scale web organizations such as Google and Amazon used NoSQL databases to focus on narrow operational goals and employ relational databases as adjuncts where high-grade data consistency is necessary.

Early NoSQL databases for web and cloud applications tended to focus on very specific characteristics of data management. The ability to process very large volumes of data and quickly distribute that data  across computing clusters were desirable traits in web and cloud design. Developers who implemented cloud and web systems also looked to create flexible data schema -- or no schema at all -- to better enable fast changes to applications that were continually updated.

There are four primary classifications for NoSQL architectures:

`Key-value stores`

Key-value stores, or key-value databases, implement a simple data model that pairs a unique key with an associated value. Because this model is simple, it can lead to the development of key-value databases, which are extremely performant and highly scalable for session management and caching in web applications. Implementations differ in the way they are oriented to work with RAM, solid-state drives or disk drives. Examples include Aerospike, Berkeley DB, MemchacheDB, Redis and Riak.

`Document databases`

Document databases, also called document stores, store semi-structured data and descriptions of that data in document format. They allow developers to create and update programs without needing to reference master schema. Use of document databases has increased along with use of JavaScript and the JavaScript Object Notation (JSON), a data interchange format that has gained wide currency among web application developers, although XML and other data formats can be used as well.  Document databases are used for content management and mobile application data handling. Couchbase Server, CouchDB, DocumentDB, MarkLogic and MongoDB are examples of document databases.

`Wide-column stores`

Wide-column stores organize data tables as columns instead of as rows. Wide-column stores can be found both in SQL and NoSQL databases. Wide-column stores can query large data volumes faster than conventional relational databases. A wide-column data store can be used for recommendation engines, catalogs, fraud detection and other types of data processing.  Google BigTable, Cassandra and HBase are examples of wide-column stores.

`Graph stores`

Graph data stores organize data as nodes, which are like records in a relational database, and edges, which represent connections between nodes. Because the graph system stores the relationship between nodes, it can support richer representations of data relationships. Also, unlike relational models reliant on strict schemas, the graph data model can evolve over time and use. Graph databases are applied in systems that must map relationships, such as reservation systems or customer relationship management. Examples of graph databases include AllegroGraph, IBM Graph, Neo4j and Titan.



More is here: [link][ns]

---

E2E Testing
-
`END-TO-END TESTING` is a type of Software Testing that validates the software system along with its integration with external interfaces. The purpose of end-to-end Test is to exercise a complete production-like scenario.

Along with the software system, it also validates batch/data processing from other upstream/downstream systems. Hence, the name "End-to-End". End to End Testing is usually executed after functional and System Testing. It uses actual production like data and test environment to simulate real-time settings. End-to-End testing is also called Chain Testing.

The chief activities involved in End to End Testing are -

Study of an end to end testing requirements
Test Environment setup and hardware/software requirements
Describe all the systems and its subsystems processes.
Description of roles and responsibilities for all the systems
Testing methodology and standards
End to end requirements tracking and designing of test cases
Input and  output data for each system


More is here: [link][e2e]

---

Unit testing
-
`Unit testing` is a software testing method by which individual units of source code, sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures, are tested to determine whether they are fit for use.[1]

Unit tests are typically automated tests written and run by software developers to ensure that a section of an application (known as the "unit") meets its design and behaves as intended.[2] In procedural programming, a unit could be an entire module, but it is more commonly an individual function or procedure. In object-oriented programming, a unit is often an entire interface, such as a class, but could be an individual method.[3] By writing tests first for the smallest testable units, then the compound behaviors between those, one can build up comprehensive tests for complex applications.[2]

To isolate issues that may arise, each test case should be tested independently. Substitutes such as method stubs, mock objects,[4] fakes, and test harnesses can be used to assist testing a module in isolation.

During development, a software developer may code criteria, or results that are known to be good, into the test to verify the unit's correctness. During test case execution, frameworks log tests that fail any criterion and report them in a summary.

Writing and maintaining unit tests can be made faster by using Parameterized Tests (PUTs). These allow the execution of one test multiple times with different input sets, thus reducing test code duplication. Unlike traditional unit tests, which are usually closed methods and test invariant conditions, PUTs take any set of parameters. PUTs have been supported by TestNG, JUnit and its .Net counterpart, XUnit. Suitable parameters for the unit tests may be supplied manually or in some cases are automatically generated by the test framework. In recent years support was added for writing more powerful (unit) tests, leveraging the concept of theories, test cases that execute the same steps, but using test data generated at runtime, unlike regular parameterized tests that use the same execution steps with input sets that are pre-defined.[5][6][7]

Why?

Unit testing can increase confidence and certainty in changing and maintaining code in the development process.
Unit testing always has the ability to find problems in early stages in the development cycle.
Codes are more reusable, reliable and clean.
Development becomes faster.
Easy to automate.

More is here: [link][ut], [link1][ut1]

---

Integration tests
-
`Integration tests` ensure that an app's components function correctly at a level that includes the app's supporting infrastructure, such as the database, file system, and network. ASP.NET Core supports integration tests using a unit test framework with a test web host and an in-memory test server.
Integration tests evaluate an app's components on a broader level than unit tests. Unit tests are used to test isolated software components, such as individual class methods. Integration tests confirm that two or more app components work together to produce an expected result, possibly including every component required to fully process a request.

These broader tests are used to test the app's infrastructure and whole framework, often including the following components:

Database
File system
Network appliances
Request-response pipeline
Unit tests use fabricated components, known as fakes or mock objects, in place of infrastructure components.

In contrast to unit tests, integration tests:

Use the actual components that the app uses in production.
Require more code and data processing.
Take longer to run.
Therefore, limit the use of integration tests to the most important infrastructure scenarios. If a behavior can be tested using either a unit test or an integration test, choose the unit test.

 Tip

Don't write integration tests for every possible permutation of data and file access with databases and file systems. Regardless of how many places across an app interact with databases and file systems, a focused set of read, write, update, and delete integration tests are usually capable of adequately testing database and file system components. Use unit tests for routine tests of method logic that interact with these components. In unit tests, the use of infrastructure fakes/mocks result in faster test execution.

 Note

In discussions of integration tests, the tested project is frequently called the System Under Test, or "SUT" for short.

"SUT" is used throughout this topic to refer to the tested ASP.NET Core app.

More is here: [link][it]

---

Trunk-Based Development
-
`Trunk-Based Development`  is a branching model for software development. Historically, it has also been called “mainline” (see later).

It requires much more concentration and rigor, than making a branch (on the shared source-control server) to suit a whim. Though you could do it without Continuous Integration (CI), as many open source projects do, for enterprise development you have to have CI linked to the trunk, enforcing multiple aspects of “that commit was good”.

In this article, I’m saying nothing about what developers do on their own workstations by way of ‘local’ branching to suit their hour by hour activities. This is all about the shared repo, where multiple developers integrate/merge their daily work for the greater good :)

Trunk-Based Development (TBD) is where all developers (for a particular deployable unit) commit to one shared branch under source-control. That branch is going to be colloquially known as trunk, perhaps even named “trunk”. Devs may, on their own dev workstations, do some multi-branch development (say with Git), but when they are “done” with a change or a bug fix, it should go back to the shared trunk. It is not “done” if it is not there - watch for that little lie of omission. See the section about pull-requests below, too.

Branches are made for a release. Developers are not allowed to make branches in that shared place. Only release engineers commit to those branches, and indeed create each release branch. They may also cherry-pick individual commits to that branch if there is a desire to do so. After a release has been superseded by another, the branch is most likely deleted.

More is here: [link][it]

---
Git Flow vs Github Flow
-

Git flow works with different branches to manage easily each phase of the software development, it’s suggested to be used when your software has the concept of “release” because, as you can see in the scheme above, it’s not the best decision when you work in Continuous Delivery or Continuos Deployment environment where this concept is missing.
Another good point of this flow is that fits perfectly when you work in team and one or more developers have to collaborate to the same feature.
But let’s take a look closer to this model.

The main branches in this flow are:

master
develop
features
hotfix
release
When you clone a GIT repository in your local folder you have immediately to create a branch from the master called develop, this branch will be the main branch for the development and where all the developers in a team will work to implement new features or bug fixing before the release.
Every time a developer needs to add a new feature he will create a new branch from develop that allow him to work properly in that feature without compromise the code for the other people in the team in the develop branch.
When the feature will be ready and tested it could be rebased inside the develop branch, our goal is to have always a stable version of develop branch because we merge the code only when the new feature is completed and it’s working.
When all the features related to a new release are implemented in the develop branch it’s time to branch the code to the release branch where there you’ll start to test properly before the final deployment.
When you branch your code from develop to release you should avoid to add new features but you should only fix bugs inside the release branch code until to you create a stable release branch.
At the end, when you are ready to push live deploy live your project, you will tag the version inside the master branch so there you can have all the different versions that you release week by week.
Apparently it could seem to much steps but it’s for sure quite safe and helps you to avoid mistakes or problem when you release, obviously to accomplish all this tasks you can find online a lots of scripts that could help you to work with Git flow in the command line or if you prefer you can use visual tools like SourceTree by Atlassian that make the dirty work for you, so you have to follow only the instructions inside the software to manage all the branches, for this reason I’ve also prepared a short video to see how use this flow with SourceTree

Github flow

So now, do you think that Github is working with Git Flow? Of course no! (Honestly I was really surprised when I read that!)
In fact they are working with a continuos deployment environment where there isn’t the concept of “release” because every time they finish to prepare a new feature they push live immediately (after the whole automation chain created in the environment).
The main concepts behind the Github flow are:

Anything in the master branch is deployable
To work on something new, create a descriptively named branch off of master (ie:new-oauth2-scopes)
Commit to that branch locally and regularly push your work to the same named branch on the server
When you need feedback or help, or you think the branch is ready for merging, open a pull request
After someone else has reviewed and signed off on the feature, you can merge it into master
Once it is merged and pushed to ‘master’, you can and should deploy immediately

More is here: [link][gf]


[pl]: https://jenkins.io/doc/book/pipeline/
[cors]: https://en.wikipedia.org/wiki/Cross-origin_resource_sharing
[pol]: http://www.thepollyproject.org/about/
[rab]: https://www.rabbitmq.com/tutorials/tutorial-one-dotnet.html
[eq]: https://github.com/EasyNetQ/EasyNetQ/wiki/Introduction
[ns]: https://searchdatamanagement.techtarget.com/definition/NoSQL-Not-Only-SQL
[e2e]: https://www.guru99.com/end-to-end-testing.html
[ut]: https://www.c-sharpcorner.com/article/a-basic-introduction-of-unit-test-for-beginners/
[ut1]: https://en.wikipedia.org/wiki/Unit_testing
[it]: https://docs.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-3.1
[tbd]: https://paulhammant.com/2013/04/05/what-is-trunk-based-development/
[gf]: https://lucamezzalira.com/2014/03/10/git-flow-vs-github-flow/