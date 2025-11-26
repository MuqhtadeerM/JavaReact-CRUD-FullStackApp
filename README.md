# JavaReact-CRUD-FullStackApp

A full‑stack CRUD (Create, Read, Update, Delete) example built with a Spring Boot (Java) backend, MySQL (Workbench) database, and a React frontend styled with Bootstrap. The project demonstrates connecting a Spring Boot REST API to a MySQL database and consuming that API from a React single-page application using React Router and component state.

## Table of contents
- About
- Features
- Technologies
- Prerequisites
- Quick start
  - Database setup (MySQL Workbench)
  - Run backend (Spring Boot)
  - Run frontend (React)
- Typical API endpoints
- Environment / configuration
- Project structure (recommended)
- Troubleshooting
- Contributing
- License

## About
This project is intended as a learning / starter template for building CRUD applications with Java (Spring Boot) and React. It uses:
- Spring Boot for the REST API and persistence (JPA / Hibernate)
- MySQL as the relational database (configured with MySQL Workbench)
- React + Bootstrap for the user interface
- React Router for client-side routing
- Axios (or fetch) for HTTP requests from the frontend to the backend

## Features
- Full CRUD on a sample entity (e.g., Employee)
- RESTful API
- MySQL persistence with JPA/Hibernate
- React UI with forms, lists, and routing
- Bootstrap for responsive styling
- Example SQL for creating the database
- Simple environment configuration for backend and frontend

## Technologies
- Java 21
- Spring Boot (2.x / 3.x)
- Spring Data JPA
- MySQL 8.0
- React 19
- Bootstrap 5
- Axios (recommended) or fetch
- Maven 

## Prerequisites
- Java SDK (21+)
- Maven 
- Node.js (21+) and npm / yarn
- MySQL server (MySQL Workbench recommended for GUI)
- Git 

## Quick start

These instructions assume the repo contains two main folders:
- backend/ (Spring Boot app)
- frontend/ (React app)

Adjust paths if your repo differs.

1. Clone the repo
   git clone https://github.com/MuqhtadeerM/JavaReact-CRUD-FullStackApp.git
   cd JavaReact-CRUD-FullStackApp

2. Database setup (MySQL Workbench)
   - Open MySQL Workbench and connect to your MySQL server.
   - Create a database for the app. Example SQL:
     CREATE DATABASE crud_app_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   - (Optional) Create a dedicated DB user and grant privileges:
     CREATE USER 'crud_user'@'localhost' IDENTIFIED BY 'your_password';
     GRANT ALL PRIVILEGES ON crud_app_db.* TO 'crud_user'@'localhost';
     FLUSH PRIVILEGES;

   - The application can also create tables for you using JPA's ddl-auto setting (see config below).

3. Configure the backend
   - The Spring Boot application reads datasource settings from application.properties or application.yml.
     Example (src/main/resources/application.properties):
     spring.datasource.url=jdbc:mysql://localhost:3306/crud_app_db?useSSL=false&serverTimezone=UTC
     spring.datasource.username=crud_user
     spring.datasource.password=your_password
     spring.jpa.hibernate.ddl-auto=update
     spring.jpa.show-sql=true

   - If using environment variables, set them as needed or edit application properties before running.

4. Run backend (Spring Boot)
   From the project root or backend folder:
   - Using Maven:
     mvn clean package
     mvn spring-boot:run
   - Or run the generated jar:
     java -jar target/<your-backend-artifact>.jar

   The backend typically starts on http://localhost:8080 by default.

5. Configure the frontend
   - Change into the frontend directory:
     cd frontend
   - Install dependencies:
     npm install
     # or
     yarn

   - Configure the API base URL. Create a .env file in the frontend directory:
     REACT_APP_API_URL=http://localhost:8080/api
     (React apps read variables prefixed with REACT_APP_.)

6. Run frontend (React)
   From the frontend folder:
   npm start
   # or
   yarn start

   The React app will typically start on http://localhost:3000 and proxy API calls to the backend (if configured), or you can call the backend directly using the REACT_APP_API_URL.

## Typical API endpoints (example)
Below are common endpoints for an "Employee" entity. Your implementation may vary.

- GET /api/employees — list all employees
- GET /api/employees/{id} — get one employee
- POST /api/employees — create a new employee
- PUT /api/employees/{id} — update an existing employee
- DELETE /api/employees/{id} — delete an employee

Use a tool like Postman or curl to test endpoints:
curl -X GET http://localhost:8080/api/employees

## Environment / configuration
Backend (application.properties or application.yml):
- spring.datasource.url
- spring.datasource.username
- spring.datasource.password
- spring.jpa.hibernate.ddl-auto (validate | update | create | create-drop)

Frontend (.env):
- REACT_APP_API_URL — base URL for API requests, e.g. http://localhost:8080/api

CORS:
- If you get CORS errors in the browser, enable CORS in Spring Boot. Example:
  @Configuration
  public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
      return new WebMvcConfigurer() {
        @Override
        public void addCorsMappings(CorsRegistry registry) {
          registry.addMapping("/api/**").allowedOrigins("http://localhost:3000");
        }
      };
    }
  }

## Project structure (suggested)
- backend/
  - src/main/java/... (Spring Boot app)
  - src/main/resources/application.properties
  - pom.xml
- frontend/
  - package.json
  - src/
    - components/
    - pages/
    - App.js
    - index.js
  - public/

Adjust these names and locations to match your repository.

## Troubleshooting
- "Cannot connect to database": check MySQL is running and connection credentials in application.properties are correct.
- "Port already in use": change server.port in application.properties or free the port.
- CORS errors: enable CORS in Spring Boot or configure a proxy in the React dev server (package.json).
- Frontend cannot reach backend: ensure REACT_APP_API_URL is correct and backend is running.

## Testing
- Backend: add unit/integration tests with JUnit and Spring Boot Test.
- Frontend: use Jest + React Testing Library for component tests.

## Deployment
- Build backend jar and run on a server or containerize with Docker.
- Build frontend production bundle with npm run build and serve via static hosting or a reverse proxy.
- Example Dockerization: create Dockerfiles for backend and frontend and orchestrate with docker-compose including a MySQL service.

## Contributing
Contributions, issues, and feature requests are welcome. Please fork the repository and submit a pull request.

## License
This project is provided as-is for learning purposes. Add a LICENSE file to specify terms (MIT, Apache 2.0, etc.).

---

If you want, I can:
- Add a ready-to-use example application.properties and .env
- Generate example SQL table schema and seed data
- Add Docker and docker-compose files to run MySQL + backend + frontend together

Tell me which of those you'd like and I will generate the files and instructions.
