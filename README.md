Introduction - Microservices with Spring Cloud
----------------------------------------------

The concept of microservices is introduced, emphasizing its significance in modern software development. Understanding the necessity of microservices is essential to grasp their role in overcoming challenges associated with traditional monolithic architectures. The inherent challenges of microservices architecture are discussed, highlighting the complexities of managing distributed systems.

Spring Cloud is presented as a solution to tackle the challenges posed by microservices architecture, providing tools and frameworks for building and managing distributed systems.

Introduction to Microservices:
-----------------------------
Microservices exhibit variability in their definitions, ranging from concise descriptions to detailed elaborations emphasizing decentralized development and lightweight communication methods. Key characteristics of microservices include their adherence to RESTful principles, utilization of small, well-defined deployable units, and integration with cloud technologies. Microservices are structured as services exposed through REST, emphasizing the importance of RESTful communication protocols. Advocating for small, carefully selected deployable units, microservices contrast with monolithic architectures, which rely on a single, large application. 

Cloud enablement allows for the dynamic scaling of microservice instances based on demand, minimizing configuration complexities and optimizing resource utilization. Production deployments illustrate the dynamic nature of Cloud-enabled architectures, showcasing multiple instances of microservices handling varying workloads.

Here course aims to explore Cloud enabling RESTful web services, focusing on architecture setup and dynamic instance management to meet evolving requirements. 

The current step provides a high-level perspective on microservices, laying the foundation for subsequent sections that delve deeper into the challenges of Cloud enabling RESTful web services. Future course modules will address challenges related to Cloud enabling RESTful web services, offering practical guidance on architecture design and management in dynamic environments.


Challenges with Microservices:
-----------------------------

1. **Bounded Context**: Defining boundaries for microservices.
2. **Configuration Management**: Handling configurations for numerous microservices.
3. **Dynamic Scaling**: Adjusting instances based on load dynamically.
4. **Visibility and Monitoring**: Centralized logging, monitoring, and identifying issues.
5. **Fault Tolerance**: Preventing cascade failure, ensuring resilience.


Introduction to Spring Cloud:
----------------------------

  - Spring Cloud is a collection of tools designed to simplify the development of distributed systems.
  - It offers solutions to common challenges encountered in cloud-based distributed architectures.

- **Spring Cloud Projects**:
  - Spring Cloud is not a single project but encompasses a variety of projects aimed at addressing different aspects of distributed systems.
  - Notable among these projects is Spring Cloud Netflix, which originated from Netflix's early exploration of microservices.
  - Other projects include Spring Cloud Config, Spring Cloud Bus, Eureka, Hystrix, Zuul, and more.

- **Key Challenges and Solutions**:
  - **Configuration Management**:
    - Managing configurations for multiple microservices and environments is complex.
    - Spring Cloud Config Server simplifies this by centralizing configurations in a Git repository, making maintenance easier.
  
  - **Dynamic Scaling**:
    - Ensuring load distribution among multiple instances of microservices dynamically.
    - Eureka Naming Server facilitates service registration and discovery, allowing microservices like CurrencyCalculationService to locate instances of CurrencyExchangeService.
    - Ribbon enables client-side load balancing to evenly distribute load among available instances.
    - Feign simplifies writing RESTful clients.
  
  - **Visibility and Monitoring**:
    - Monitoring and tracing requests across microservices is crucial.
    - Spring Cloud Sleuth assigns IDs to requests for tracking, and Zipkin Distributed Tracing helps trace requests across components.
  
  - **Common Features Handling**:
    - Implementing common features like logging, security, and analytics across microservices can be tedious.
    - API Gateways like Netflix Zuul offer solutions to streamline this process.
  
  - **Fault Tolerance**:
    - Ensuring system resilience when services fail is essential.
    - Hystrix helps configure default responses when a service is unavailable.
	

Understanding Advantages of Microservices Architectures:
-------------------------------------------------------

Microservice architectures offer several benefits over traditional monolithic approaches.

- **Adaptation of New Technology and Processes**:
  - Microservices enable easy adoption of new technologies and processes.
  - Unlike monolithic applications, where all components are built using the same technology stack, microservices allow flexibility.
  - Each microservice can be built using different technologies, facilitating integration of new languages or frameworks as needed.
  - This adaptability allows developers to leverage emerging technologies and benefits offered by new languages without major restructuring.

- **Dynamic Scaling**:
  - Microservices architecture supports dynamic scaling, crucial for applications with fluctuating traffic.
  - For example, during peak seasons like Black Friday for an online shopping app, the load can spike significantly.
  - With microservices deployed on cloud platforms, they can scale up or down based on demand.
  - This dynamic scaling ensures optimal resource utilization and enhances performance during peak times while minimizing costs during periods of low activity.

- **Faster Release Cycles**:
  - Breaking an application into smaller, decoupled components makes it easier to release updates and new features.
  - Compared to monolithic applications, where changes require extensive testing and deployment processes, microservices allow for faster release cycles.
  - Developers can independently develop, test, and deploy microservices, reducing the risk of disruptions to the entire system.
  - This agility enables businesses to respond quickly to market demands and deliver new features faster, gaining a competitive edge.
  
  
Standardization and URLs in Microservices:
-----------------------------------------

In the Microservices, multiple components will be developed and installed, emphasizing the need for standardizing ports and managing URLs.

- **Port Standardization**:
  - Standardizing ports ensures consistency and clarity in running different applications.
  - A list of ports for each component is provided. Each of these application we will look as an excersize

| Application                        | Port(s)              |
|-----------------------------------|----------------------|
| Limits Service                    | 8080, 8081, ...     |
| Spring Cloud Config Server       | 8888                |
| Currency Exchange Service        | 8000, 8001, 8002, ..|
| Currency Conversion Service      | 8100, 8101, 8102, ...|
| Netflix Eureka Naming Server    | 8761                |
| Netflix Zuul API Gateway Server | 8765                |
| Zipkin Distributed Tracing Server| 9411                |

  - From above example, Limits Service uses ports 8080 and 8081, Currency Exchange Service uses port 8000, and Currency Conversion Service uses port 8100.
  - Default ports are specified for Spring Cloud Config Server (8888), Netflix Eureka Naming Server (8761), Zuul API Gateway Server (8765), and Zipkin Distributed Tracing Server (9411).
  - It's essential to use the correct ports for each component to avoid confusion and ensure seamless integration.

- **URL Management**:
  - With numerous components, managing URLs becomes crucial, especially considering their complexity.
  - If encountering issues with URLs, referring to this section can help in troubleshooting and creating accurate URLs.

| Application                            | URL                                                            |
|---------------------------------------|----------------------------------------------------------------|
| Limits Service                        | http://localhost:8080/limits                                   |
|                                       | http://localhost:8080/actuator/refresh (POST)                  |
| Spring Cloud Config Server            | http://localhost:8888/limits-service/default                   |
|                                       | http://localhost:8888/limits-service/dev                       |
| Currency Converter Service - Direct Call | http://localhost:8100/currency-converter/from/USD/to/INR/quantity/10 |
| Currency Converter Service - Feign    | http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000 |
| Currency Exchange Service             | http://localhost:8000/currency-exchange/from/EUR/to/INR       |
|                                       | http://localhost:8001/currency-exchange/from/USD/to/INR       |
| Eureka                                | http://localhost:8761/                                         |
| Zuul - Currency Exchange & Exchange Services | http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR |
|                                       | http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10 |
| Zipkin                                | http://localhost:9411/zipkin/                                  |
| Spring Cloud Bus Refresh              | http://localhost:8080/actuator/bus-refresh (POST)             |


  - Particularly beneficial when dealing with complex URLs, such as those involving Currency Exchange Service or Currency Conversion Service through Zuul.

Port standardization and URL management are vital aspects of developing and deploying microservices. Consistent use of standardized ports and effective URL management enhance clarity, organization, and troubleshooting throughout the development process. We should pay attention to these aspects to ensure smooth execution and understanding of microservices development.
