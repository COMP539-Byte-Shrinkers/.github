---

# URL Shortener Service

The `backend` folder contains the backend code for a URL shortener service built with Spring Boot and Maven. It allows users to shorten URLs and retrieve the original URLs using both authenticated and guest endpoints.

## Setup Instructions

### Prerequisites

- Java JDK 11+
- Maven
- Google Cloud SDK

### Authentication

First, authenticate with Google Cloud using the provided service account JSON key file. **Ensure this JSON key file is kept secure and not exposed publicly**:

```bash
gcloud auth activate-service-account team5-746@rice-comp-539-spring-2022.iam.gserviceaccount.com --key-file="PATH_TO_YOUR_SECURE_KEY_FILE"
export GOOGLE_APPLICATION_CREDENTIALS="PATH_TO_YOUR_SECURE_KEY_FILE"
```

Replace `PATH_TO_YOUR_SECURE_KEY_FILE` with the path where your key file is securely stored. Do not commit this key file to your version control system.

### Building and Running the Application

Compile the application and clean previous builds using Maven:

```bash
mvn clean compile
```

To run the application, use the following command:

```bash
mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8080
```

### Google Cloud Platform Deployment

For details on deploying this Maven project to Google Cloud Platform, refer to our **GCP Deployment Guide**. This guide provides a semi-detailed walkthrough of two different deployment methods suited for this application:

[View the GCP Deployment Guide](https://docs.google.com/document/d/1cCWQ3TKTra0tqCKrBMddgVwaignkB5H9b94HNTn3eN8/edit)

Ensure you have the appropriate permissions to access this document.

## API Endpoints

The service provides the following RESTful endpoints:

### Guest Endpoints

- **POST /guest/shorten**: Allows guests to shorten URLs without authentication.
  - **Input**: JSON containing `originalUrl`.
  - **Response**: JSON containing `shortUrl` and result status.

- **GET /guest/retrieve/{shortUrl}**: Retrieve the original URL for a given short URL without authentication.
  - **Response**: JSON containing the original URL or error message.

### Authenticated Endpoints

- **POST /shorten**: Allows authenticated users to shorten URLs. Links shortened URLs to their account.
  - **Input**: JSON containing `originalUrl`.
  - **Response**: JSON containing `shortUrl` and result status.

- **GET /retrieve/{shortUrl}**: Retrieve the original URL for a given short URL with authentication.
  - **Response**: JSON containing the original URL or error message.

- **GET /history**: Fetches a history of URLs shortened by the authenticated user.
  - **Response**: JSON containing a list of URLs associated with the user's account.

- **GET /email**: Provides the email address of the authenticated user.
  - **Response**: JSON containing the user's email.

### Registration and Authentication

- **POST /register**: Registers a new user with an email and password.
  - **Input**: JSON containing `email` and `password`.
  - **Response**: JSON confirming registration status and user email.

### Redirect Endpoint

- **GET /{shortUrl}**: Redirects to the original URL if it has not expired.
  - **Response**: Redirect to the original URL or an error page.

## Cross-Origin Resource Sharing (CORS)

The application allows cross-origin requests from the following origins:

- `http://localhost:8080`
- `http://localhost:3000`
- `https://team5-dot-rice-comp-539-spring-2022.uk.r.appspot.com`
- `http://byte-shrinker-v2.surge.sh`
- `https://byte-shrinker-v2.surge.sh`

## Security

This application uses Spring Security to manage authentication and protect endpoints that require user identification.

## Complete Service and Demo

The final service, including the frontend, is available at:

[Visit Byte Shrinker v2](https://byte-shrinker-v2.surge.sh/)

For a visual demonstration of how the service works, check out our presentation and demo video:

[Watch the presentation and demo](https://docs.google.com/presentation/d/1X8FfI64Z5j1rrbG3wWKXBGAia_R5g79AnVvDKo4Sth8/edit?usp=drive_link)

---

