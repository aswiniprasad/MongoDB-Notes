# MongoDB Notes
Notes on modeling guidelines for designing data models when working with document database (NoSQL- MongoDB).

## What is MongoDB (Just a brief intro)?
* MongoDB is a document oriented NoSQL databse used for high volume data storage in a flexible way.
* We call tables and rows in traditional relational databses, whereas in MongoDB we call them as collections and documents.
* These documents consist of key-value pairs which are the primary unit of data in MongoDB.
* This document structure is kind of more in line with how we construct classes and their objects in programming languages.
* The rows doesn't need to have a schema defined beforehand, We can create on the fly.
* The data model allows to represent hierarchical relationships, to store arrays and more complex structures and are very scalable.

### When designing the data models, the primary question that one can think off is "to embed or not to embed"?

##### Is the embedded data wanted 80% of the time, when you have the outer or other related object?
* If yes, then it is better to embed data in the containing document.

#### How often do you want the embedded data without the containing document?
* If you are in that sort of situation, where you require embedded data more often than the containing document as a whole, then it is better to put the data in a seperate collection and not embedded.

#### Is the embedded data(document) a bounded set?
* I mean, is the embedded document continuously grow in time or not? 
  - If yes, then it is not a good idea to embed that kind of data.
* Because that document should just grow & grow, and it could make the containing document so large and when you retrieve it from the database, actually the network traffic and this data traffic would be a problem.
* So, the idea is if it is an unbounded set, do not want to embed it.

#### Is that bound small?
* The reason is, these documents in MongoDB are limited to 16 MB. So, no single record in MongoDB can be larger than 16 MB.
* This is not a limitation of MongoDB, Infact this is them trying to protect you from yourself.
* The maximum document size helps ensure that a single document cannot use excessive amount of RAM or, during transmission, excessive amount of bandwidth.
* Reading larger size documents from database over the network will destroy the performance of the database. So, having these very large records is a problem, so they actually set an upper bound on how large that can be. It's a best practice to always keep these documents in ten's or thousand's of kilo bytes.
* To store documents larger than the maximum size, MongoDB provides the GridFS API.
* So, having small amount of data sets means that your documents wont grow into huge monolithic sets that are hard to work with.

#### How varied are your queries?
* One of the things that you do with document databases is you try to structure the documents to answer the most common questions in the most well structured way.
* If it's like a data warehouse asking all kinds of questions from all different sorts of applications, then trying to understand what is the right way to build my documents, so it matches the queries that i typically do are the ones that i need to be really quick and fast.. that becomes hard because there is all these different queries and the way you model for one is exactly the opposite of the way you model for the other.
* So, depending how focused your application is or how many applications are using your database you will have a different answer for this question.
* The more specific your queries are,  the more likely you have to embed things and structure them exactly to match this queries.
