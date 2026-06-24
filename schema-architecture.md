# Smart Clinic Management System Architecture

## Architecture Summary

This Spring Boot application uses both MVC and REST controllers. Thymeleaf templates are used for the Admin and Doctor dashboards, while REST APIs handle appointments, patient dashboards, and patient records. The application uses two databases: MySQL for structured data such as patients, doctors, appointments, and administrators, and MongoDB for prescription documents.

All requests pass through controllers and are processed by a shared service layer. The service layer applies business logic and communicates with repositories. MySQL data is managed through JPA entities, while MongoDB data is managed through document models.

## Numbered Flow of Data and Control

1. Users access dashboards or application modules through a browser or API client.
2. Requests are routed to either Thymeleaf controllers or REST controllers.
3. Controllers send requests to the service layer for processing.
4. The service layer applies business rules and calls the required repositories.
5. Repositories interact with MySQL or MongoDB databases.
6. Retrieved data is mapped into JPA entities or MongoDB document models.
7. The application returns HTML pages through Thymeleaf or JSON responses through REST APIs.
