# spring-boot-microservices
the Programming Techie microservices application empowers seamless product management, order processing, and inventory control through secure API access, real-time event-driven communication via Kafka, and built in fault tolerance for a robust and efficient system. 

## Tools Used
IntelliJ, Docker Desktop, MySQL Workbench, Postman API, Web browser.

## Features
- Designed individual microservices using Spring Boot and Gradle to manage product catalogs, orders and inventory efficiently by interaction between different services using Web Client. 
- Ensured communication between microservices via RESTful APIs or messaging systems like Kafka. 
- Implemented service discovery using Eureka to dynamically locate services within the network. 
- Created a single-entry point for clients to access multiple microservices using Spring Cloud Gateway. 
- Integrated Keycloak for OAuth2-based authentication and authorization. 
- Used Resilience4j to handle faults and latency tolerance between microservices. 
- Utilized Zipkin to monitor and trace requests across microservices using TraceId. 
- Implemented asynchronous communication and event-driven patterns using Kafka and Avro serialization. 
- Used cloud-based Atlas MongoDB and MySQL for the backend database.


## Installation

To run this project locally, follow these steps:

1. Clone the repository:

    git clone https://gitlab.com/manoj-jeenu/spring-boot-microservices.git


2. Navigate to the project directory:
   
    cd spring-boot-microservices


3. Build the project using Gradle:

    ./gradlew build

4. Run the project:

    java -jar build/libs/spring-boot-microservices-0.0.1-SNAPSHOT.jar

## Usage
- start Zipkin via Docker by running the command [docker run -d -p 9411:9411 openzipkin/zipkin]
- start Keycloak vai Docker by running the commandd [docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:24.0.4 start-dev]
- After starting the Login to Keycloak with usersname - [admin] and password [admin].
- Create the realm under keycloak by providing the Realm name.
- Create client under clients with type [OpenID Connect] and provide the clientID name and click on next.
- Enable [Client authentication] , uncheck/Unselect if [Direct access grants] is checked and checkbox/select the [Standard flow] and [Service account roles] under [Authentication flow] and click on next.
- Add the [Valid redirect URIs]  - http://localhost:8080/login/oauth2/code/{Realm-name}
- Add the [Web origins] - http://localhost:8080 and click on save.
- open the client created and navigate to the tab [credentials] and copy the [Client Secret] Key.
- use this [Client Secret] under the POST request in postman 
- Navigate to Authorization tab select the [Auth type] as [OAuth 2.0] . Scrolls down to the [Configure New Token] tab and set the following parameters
    - Token Name : Provide a token name (Ex : Token)
    - Grant type : Client Credentials
    - Access Token URL : KeyCloak -> Realm setting -> Endpoints -> OpenID Endpoint Configuration -> "token_endpoint": "http://localhost:8080/realms/spring-boot-microservices/protocol/openid-connect/token"
    - Client ID : Enter the cleint created before.
    - Client Secret : paste the [cleint secret] key copied under credentials.
- click on [Get new Access Token] and use the token to hit the servcie and Bhoommm!.
- Run the [docker compose up - d ] to run the Images in docker-compose.yml file and [docker compose down] to terminate the servers.

## Endpoints
- Product - Service (MySQL database)
    - POST  - http://localhost:8081/api/product
    - GET   - http://localhost:8081/api/product
- Order-Service (MySQL database)
    - POST  - http://localhost:8082/api/order
    - GET   - http://localhost:8082/actuator/circuitbreakerevents
    - GET   - http://localhost:8082/actuator/health
    - GET   - http://localhost:8082/actuator
- Inventory - Service (MongoDB database)
    - GET   - http://localhost:8083/api/inventory/{sku-code}
    - GET   - http://localhost:8083/api/inventory
- Discovery - Server (eureka)
    - GET   - http://localhost:8761/
- API - Gateway (OAuth2)
    - POST  - http://localhost:8084/api/order
    - POST  - http://localhost:8084/api/product
    - GET   - http://localhost:8084/api/product
    - POST  - http://localhost:8084/api/order
    - GET   - http://localhost:8084/actuator/circuitbreakerevents
    - GET   - http://localhost:8084/actuator/health
    - GET   - http://localhost:8084/actuator
    - GET   - http://localhost:8084/api/inventory/{sku-code}
    - GET   - http://localhost:8084/api/inventory

## Getting started

To make it easy for you to get started with GitLab, here's a list of recommended next steps.

Already a pro? Just edit this README.md and make it your own. Want to make it easy? [Use the template at the bottom](#editing-this-readme)!

## Add your files

- [ ] [Create](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#create-a-file) or [upload](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#upload-a-file) files
- [ ] [Add files using the command line](https://docs.gitlab.com/ee/gitlab-basics/add-file.html#add-a-file-using-the-command-line) or push an existing Git repository with the following command:

```
cd existing_repo
git remote add origin https://gitlab.com/manoj-jeenu/spring-boot-microservices.git
git branch -M main
git push -uf origin main
```

## Integrate with your tools

- [ ] [Set up project integrations](https://gitlab.com/manoj-jeenu/spring-boot-microservices/-/settings/integrations)

## Collaborate with your team

- [ ] [Invite team members and collaborators](https://docs.gitlab.com/ee/user/project/members/)
- [ ] [Create a new merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
- [ ] [Automatically close issues from merge requests](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
- [ ] [Enable merge request approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/)
- [ ] [Set auto-merge](https://docs.gitlab.com/ee/user/project/merge_requests/merge_when_pipeline_succeeds.html)

## Test and Deploy

Use the built-in continuous integration in GitLab.

- [ ] [Get started with GitLab CI/CD](https://docs.gitlab.com/ee/ci/quick_start/index.html)
- [ ] [Analyze your code for known vulnerabilities with Static Application Security Testing (SAST)](https://docs.gitlab.com/ee/user/application_security/sast/)
- [ ] [Deploy to Kubernetes, Amazon EC2, or Amazon ECS using Auto Deploy](https://docs.gitlab.com/ee/topics/autodevops/requirements.html)
- [ ] [Use pull-based deployments for improved Kubernetes management](https://docs.gitlab.com/ee/user/clusters/agent/)
- [ ] [Set up protected environments](https://docs.gitlab.com/ee/ci/environments/protected_environments.html)

<!---
## Badges
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals
Depending on what you are making, it can be a good idea to include screenshots or even a video (you'll frequently see GIFs rather than actual videos). Tools like ttygif can help, but check out Asciinema for a more sophisticated method.

## Installation
Within a particular ecosystem, there may be a common way of installing things, such as using Yarn, NuGet, or Homebrew. However, consider the possibility that whoever is reading your README is a novice and would like more guidance. Listing specific steps helps remove ambiguity and gets people to using your project as quickly as possible. If it only runs in a specific context like a particular programming language version or operating system or has dependencies that have to be installed manually, also add a Requirements subsection.

## Usage
Use examples liberally, and show the expected output if you can. It's helpful to have inline the smallest example of usage that you can demonstrate, while providing links to more sophisticated examples if they are too long to reasonably include in the README.

## Support
Tell people where they can go to for help. It can be any combination of an issue tracker, a chat room, an email address, etc.

## Roadmap
If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing
State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.

## Project status
If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.
-->