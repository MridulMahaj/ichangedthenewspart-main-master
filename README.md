## Running with Docker

This project includes Docker and Docker Compose setup for easy containerized deployment.

### Requirements
- **Java Version:** Uses Eclipse Temurin JDK 17 (as specified in the Dockerfile)
- **Build Tool:** Maven Wrapper (`mvnw`) is included and used for building the project

### Build and Run Instructions
1. **Build and Start the Service**
   - From the project root, run:
     ```sh
     docker compose up --build
     ```
   - This will build the application using the provided Dockerfile and start the container.

2. **Service Details**
   - **Service Name:** `java-ichangedthenewspart-main`
   - **Exposed Port:** `8080` (Spring Boot default)
   - **Container User:** Runs as a non-root user for security
   - **Network:** Service is attached to the `backend` bridge network

### Environment Variables
- No required environment variables are specified in the Dockerfile or compose file.
- If you need to add environment variables, uncomment the `env_file` line in `docker-compose.yaml` and provide a `.env` file in the project root.

### Special Configuration
- The build skips tests for faster container creation (`-DskipTests` in Dockerfile)
- JVM is configured for container resource awareness (`JAVA_OPTS`)
- No external database or cache is configured by default

---

*This section was updated to reflect the current Docker setup for the project. For further details, refer to the Dockerfile and docker-compose.yaml in the repository.*
