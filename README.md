# Back-End Engineer Interview challenge

DataOne Innovation Labs interview challenge for Full Stack Developer Candidate

This repository contains an intro challange for full stack developers who want to join [DataOne Innovation Labs](http://dataone.io).

### So you want to prove you're worthy to join DataOne? Awesome!

**Here you go:**
* Read below insturctions carefully
* Setup local environment in your machine and perform this task
* Send us your submission through a cloud hosting service (Link to Google Drive, Dropbox etc.) 
* Make sure you put a README file with detailed instructions and all assumptions to run your code
* When you think you finished with all the tasks send us an email with your submission link.

**Task 1:**

The json transformer service is a webservice which accepts a JSON payload (via an HTTP PUT or HTTP POST action) and performs an action on it based on the endpoint the payload is received on.  The JSON transformer service has three endpoints

| Endpoint        | Function           | HTTP Verb  |
| ------------- |-------------| -----|
| `/alpha`     | Alphabetize the keys in the request JSON payload and return the resulting JSON back in the HTTP response | `PUT` |
| `/flatten`      | Flatten any JSON Arrays in the request JSON payload (comma separated) such that the resulting JSON does not contain any JSON Arrays        |   `POST` |
| `/status`      | Obtains the health status of the system and responds with the details in the HTTP response | `GET` |

## examples
### /alpha
**input**
`HTTP PUT /alpha`
```
{
  "fruit":"apple",
  "animal":"zebra",
  "city-list":["sunnyvale","sanjose"]
}
```
**output**
```
{
  "animal":"zebra",
  "city-list":["sunnyvale","sanjose"],
  "fruit":"apple"
}
```

### /flatten
**input**
`HTTP PUT /flatten`
```
{
  "fruit":"apple",
  "animal":"zebra",
  "city-list":["sunnyvale","sanjose"]
}
```
**output**
```
{
  "fruit":"apple",
  "animal":"zebra",
  "city-list":"sunnyvale,sanjose"
}
```

### /status
**input**
`HTTP GET /status`

**output**
```
{
  "mem-used-pct" : 83.6,
  "disc-space-avail" : [
                         { "discname" : "/dev/SDA1", "availbytes" : "12345000"},
                         { "discname" : "/dev/SDA2", "availbytes" : "12345000"}
                       ],
  "cpu-used-pct" : 55.0
}
```

**Task 2:**

Our microservice architecture has a service to create and manage products. We now would like to add another microservice that offers search and filter capabilities for products. To quickly provide a working endpoint to our frontend team, we agreed on the following details.

## Read Data from In-memory (H2) Database

The service should connect to In-memory H2 store, where it can read products with the following structure:

```JSON
{
	"id": 1,
	"name": "Product A",
	"price": 12.99,
	"brand": "Brand A",
	"onSale": true
}
```
Pre-load database with at least 10 products.

Expected Response
- 
Our Frontend Team expects a response matching the following requirements

- All products are returned
- Products are grouped by `brand`, sorted alphabetically
- Property `brand` should be omitted on products
- Products inside a `brand` should be sorted ascending by `price`
- Property `onSale` should be converted to a property `event` of type String with the value "ON SALE"

```JSON
{
	"Brand A" : [{
		"id": 1,
		"name": "Product A",
		"price": 12.99,
		"event": "ON SALE"
	},
	{
		"id": 2,
		"name": "Product B",
		"price": 7.99
	}],
	"Brand B" : [{
		"id": 3,
		"name": "Product C",
		"price": 14.99
	},
	{
		"id": 4,
		"name": "Product D",
		"price": 10.99
	}]
}
```

# Technical Requirement  

We expect:  
 - a JVM based solution using JDK 8 or higher
 - that is cloud ready
 - that can be build and executed on any environment ( e.g. local, jenkins )
 - with tests verifying the given requirements 
 - and  a versioned code base

## Freedom of Tools and Technology

Microservice architecture give us the freedom to pick the tools best suited for our skills and requirements.
To quickly get started you can use this https://start.spring.io based skeleton. 

However **we suggest you to use the tools and technologies you are comfortable with**. The solution won't be better just because you used the skeleton. 


You need to implement these two tasks in two separate microservices. This should be implemented using Maven and Java and must include tests to prove that your service is working correctly.  Attention should be paid to both happy path and error conditions as well as documentation of the service.

Required artifacts:
- Code with test cases.
- Readme.md file for installation and running.
- API Documentation. (Swagger is preferrable).
- A postman collection to test all implemented API Endpoints
- Dockerfile (Nice to have)
- Docker Compose, Docker Swarm or Kuberntes orchestration. (Nice to have)
