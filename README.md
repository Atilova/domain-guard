# Domain Guard System
Domain Guard System is a project demonstrating microservice architecture utilizing **Clean Architecture** principles in its services. The project is designed to provide consumers with domain data and information, aggregating data from different sources into a standardized response. The system can be expanded with additional services, such as port scanners, IP checkers, and health check functionalities. Currently, the project supports domain DNS records (present now), history records (past), and subdomains info including _A_, _AAAA_, _MX_, _NS_, _TXT_, and _SOA_ records. All services follow the same architecture principles and patterns, adhering to **DDD (Domain Driven Design)** and **SOLID** principles for scalability. Services communicate via RabbitMQ message broker.


## Implemented services
### 1. Securitytrails-accounts
The securitytrails-accounts service is responsible for obtaining SecurityTrails accounts using Selenium to bypass CAPTCHA. Each free account provides up to 50 free requests per month. This service supports a Flask development HTTP server.

`Responsibilities`
- Obtain new SecurityTrails accounts.

`Read More` https://github.com/atilova/domain-guard-securitytrails/


### 2. Aggregator
The aggregator service utilizes other services or resources to aggregate domain summaries into a single output. It communicates with the securitytrails-accounts service to obtain new accounts, stores accounts in a PostgreSQL database, and manages them. This service interacts with the SecurityTrails API to provide summary information. Future functionalities include port scanning, IP checking, and health checking.

`Responsibilities`
- Gather information
- Interact with APIs
- Implement new features

`Read More` https://github.com/Atilova/domain-guard-aggregator/

### 3. Dashboard
The Dashboard service interacts with the aggregator via RPC calls to provide users with the best experience following data. It offers an open API for performing requests and implements JWT cookies authentication for private user features such as daily/regular scanning, changes checker, and history search. It utilizes Celery for scheduled tasks and REST API for robust API interactions.

`Features`
- RPC calls to the aggregator
- Open API
- JWT cookies authentication
- Daily/regular scanning
- Changes checker
- History search

`Read More` https://github.com/Atilova/domain-guard-dashboard/


## Future services
### 4. User Notification Bot
A Telegram bot service for sending domain updates, interacting with the Dashboard service.

### 5. UI-UX Dashboard Frontend
A frontend application utilizing VueJS to provide a user interface for the dashboard.


## Project Todos
* Provide a main docker-compose file to start development and production environments,   setting up networks, Redis, and RabbitMQ services.
* Setup CI/CD pipelines with GitHub Actions and deploy a test version to AWS.
* Include Dockerfile in each service for environment builds.
* Cover main parts of the application with pytest to enhance proper data manipulation and consistency of an API.

## Summary
Domain Guard System is a robust project built on microservice architecture and Clean Architecture principles, offering scalable and modular domain data services. With current and future services designed for comprehensive domain management and notification, the project aims to provide extensive functionalities and a seamless user experience.