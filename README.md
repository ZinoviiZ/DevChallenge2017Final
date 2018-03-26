# DevChallengeFinal
Application for DevChallenge2017 final, backend nomination, middle-senior category. </br>
I've taken 2nd place in that compatition. </br>
You can check this result in public lists on the website:</br>
https://devchallenge.it/ </br>

## DevChallenge
All-Ukrainian software development championship among junior, middle and senior programmers. The championship takes place in 3 stages: Qualification, Semifinal and offline Finals in Kyiv. Participants compete in eleven nominations in three directions: Web, Mobile, Game. Each nomination has 2 categories: Pro (Senior, Middle-to-Senior) and Standard (Middle, Junior-to-Middle).
At the final, the tasks were from the partner Amazon.

### Task
You can find the task in **back-endprofinaltaskdevchallenge11.pdf**

# Solution

### Run solution:
`docker-compose up` </br>

**This command is running next applications:**
- mongoDB </br>
- config service </br>
- registry service </br>
- main service </br>
- callcenter - two replicas </br>

I've chosen microservice architecture with RESTful microservices. I won't write about all advantages of this approach. </br>
I've written this microservice patterns: </br>
- ServiceConfig - microservice for saving all microservices settings.</br>
- ServiceRegistry - using Eureka service registry by Netflix. After running open - localhost:8010/ </br>
- CircuitBrikear and LoadBalancer - after running, open http://localhost:8001/hystrix, write http://localhost:8001/hystrix.stream in the field and push button "Monitor System". </br>
Added Swagger API for testing rest services. After running open localhost:8001/swagger-ui.html </br>

As my DB I've chosen MongoDB - open-source cross-platform document-oriented database. I think it's working well for tasks like this. </br>

# System architecture:
All requests come to server_main - gateway, after it's balancing with two replicas call center microservices. For scalable we can run more microservices. If some microservices will fall, the gateway will use another microservice. If all microservices will fall, a gateway will response customer-readable message. Call center microservice finds employees with requirements and chose optimized employees with fewer expertise areas in EmployeeService.class in server_client(call center) module. Not enough time for writing more tests, so I wrote tests for main logic.</br>

**I've change response representation(comparing to instruction) cos I think it's the better approach for scalable microservices.**

#### For scalable systems:
We should run few ServiceConfig and ServiceRegistry replicas.</br>
All class architecture was written for future scaling and with OOP and SOLID principles.</br>
