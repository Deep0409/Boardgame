# BoardgameListingWebApp

## Description

**Board Game Database Full-Stack Web Application.**
This web application displays lists of board games and their reviews. While anyone can view the board game lists and reviews, they are required to log in to add/ edit the board games and their reviews. The 'users' have the authority to add board games to the list and add reviews, and the 'managers' have the authority to edit/ delete the reviews on top of the authorities of users.  

## Technologies

- Java
- Spring Boot
- Amazon Web Services(AWS) EC2
- Thymeleaf
- Thymeleaf Fragments
- HTML5
- CSS
- JavaScript
- Spring MVC
- JDBC
- H2 Database Engine (In-memory)
- JUnit test framework
- Spring Security
- Twitter Bootstrap
- Maven

## Features

- Full-Stack Application
- UI components created with Thymeleaf and styled with Twitter Bootstrap
- Authentication and authorization using Spring Security
  - Authentication by allowing the users to authenticate with a username and password
  - Authorization by granting different permissions based on the roles (non-members, users, and managers)
- Different roles (non-members, users, and managers) with varying levels of permissions
  - Non-members only can see the boardgame lists and reviews
  - Users can add board games and write reviews
  - Managers can edit and delete the reviews
- Deployed the application on AWS EC2
- JUnit test framework for unit testing
- Spring MVC best practices to segregate views, controllers, and database packages
- JDBC for database connectivity and interaction
- CRUD (Create, Read, Update, Delete) operations for managing data in the database
- Schema.sql file to customize the schema and input initial data
- Thymeleaf Fragments to reduce redundancy of repeating HTML elements (head, footer, navigation)

## How to Run

1. Clone the repository
2. Open the project in your IDE of choice
3. Run the application
4. To use initial user data, use the following credentials.
  - username: bugs    |     password: bunny (user role)
  - username: daffy   |     password: duck  (manager role)
5. You can also sign-up as a new user and customize your role to play with the application! 😊



CI/CD Pipeline Implementation 
Prometheus Dashboard
<img width="1357" height="668" alt="image" src="https://github.com/user-attachments/assets/c52276fd-fd21-4748-af34-ba00c9227df4" />

Grafana Dashboard for k8s Monitoring
<img width="1344" height="676" alt="image" src="https://github.com/user-attachments/assets/80a79499-8323-413b-a46c-c70295026afe" />

Grafana Dashboard for Jenkins Monitoring
<img width="1335" height="677" alt="image" src="https://github.com/user-attachments/assets/5a802e22-0e1d-4db0-8495-a62398d1343b" />

Grafana Dashboard for Node Monitoring
<img width="1342" height="681" alt="image" src="https://github.com/user-attachments/assets/0eecda45-f107-4c8d-8bcb-6e5232721d7c" />
