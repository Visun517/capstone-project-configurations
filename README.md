# ⚙️ Capstone Project Configurations

Welcome to the configuration repository for the **ECA Campus Management System**. This repository serves as the central configuration source for the Spring Cloud Config Server, storing externalized configurations for all platform components and business microservices.

## 🎓 1. Student Information

| Attribute | Details |
| :--- | :--- |
| **Name** | Visun Prabodha |
| **Student Number** | 241711009 |
| **Slack Handle** | Visun Prabodha |
| **GCP Project ID** | `visun-gcp-lab` |

## 📖 2. Project Description

The **ECA Campus Management System** relies on a distributed microservices architecture. To manage configurations across multiple environments and services efficiently, this repository acts as the single source of truth. It utilizes **Spring Cloud Config Server** to serve configuration files dynamically to microservices at startup. 

By externalizing these configurations, we decouple configuration management from the application code, enabling seamless updates across different environments.

## 🛠️ 3. Technology / Format Stack

*   **Format:** YAML (`.yaml`)
*   **Architecture Pattern:** Externalized Configuration
*   **Framework/Tools:** Spring Cloud Config, Spring Boot

## 📂 4. Configuration Structure

Below is the repository structure representation for the configuration files:

```text
📦 capstone-project-configurations
 ┣ 📜 application.yaml
 ┣ 📜 api-gateway.yaml
 ┣ 📜 student-service.yaml
 ┣ 📜 program-service.yaml
 ┗ 📜 enrollment-service.yaml
```

### 📄 Configuration File Breakdown

| File Name | Purpose / Key Configurations Included |
| :--- | :--- |
| 🌐 `application.yaml` | **Global Configurations:** Contains shared properties across all services, such as the Eureka `defaultZone` for service discovery and base logging levels. |
| 🚪 `api-gateway.yaml` | **API Gateway Routing & Security:** Defines routing logic (Predicates & Filters), global CORS configurations for cross-origin requests, and maximum file upload size limits. |
| 🧑‍🎓 `student-service.yaml` | **Student Microservice:** Includes PostgreSQL database connection properties, Tomcat swallow size limits, and the Google Cloud Storage bucket name (`app.storage.bucket-name`). |
| 📚 `program-service.yaml` | **Program Microservice:** Stores PostgreSQL database connection details specific to academic program data management. |
| 📝 `enrollment-service.yaml`| **Enrollment Microservice:** Contains MongoDB connection details for handling document-based enrollment records. |

## 🚀 5. Usage Instructions

### Connecting the Config Server
To utilize this repository, ensure your **Spring Cloud Config Server** is configured to point to this Git repository URL in its configuration file:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/[your-username]/capstone-project-configurations.git
          default-label: main
```

### Consuming Configurations in Microservices
Each microservice in the ECA Campus Management System must include the `spring-cloud-starter-config` dependency.

Configure each microservice to fetch its respective `.yaml` file by specifying the Config Server URI and its application name:

```yaml
spring:
  config:
    import: "optional:configserver:http://localhost:8888"
  application:
    name: student-service # This maps directly to student-service.yaml
```
