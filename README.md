# E-commerce Notification Service

## Overview

The **E-commerce Notification Service** is responsible for sending notifications to users. This includes order confirmations, payment status updates, and promotional messages. The service integrates with third-party messaging providers (e.g., email, SMS) and interacts with other microservices such as the **E-commerce Order Service** and **E-commerce Payment Service**.

## Features

- **Email Notifications**: Send order confirmations, shipping updates, and more via email.
- **SMS Notifications**: Optional SMS alerts for users.
- **Promotional Notifications**: Send marketing emails and promotions.
- **Inter-Service Communication**: The service communicates with the **Order Service** and **Payment Service** to notify users of order and payment status changes.

## Technologies Used

- **Java**
- **Spring Boot**
- **Maven** (for dependency management)
- **PostgreSQL** (for storing notification data)
- **Third-Party APIs** (for email and SMS services)

## Prerequisites

Before running this service, ensure you have the following:

- **Java JDK 11 or higher**
- **Maven** (for building the project)
- A running **PostgreSQL** database (or other supported database).
- Access to third-party notification services like **Twilio** (for SMS) or **SendGrid** (for emails).
- Access to the relevant microservices (Order Service, Payment Service).

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/juansebstt/ecommerce-notification-service.git
    ```

2. Navigate to the project directory:

    ```bash
    cd ecommerce-notification-service
    ```

3. Build the project using Maven:

    ```bash
    mvn clean install
    ```


## Configuration

You need to configure the database, messaging services, and other application settings in your `application.yml` or `application.properties` file.

### Sample Configuration

```yaml
server:
  port: 8085

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/ecommerce_notification_db
    username: yourUsername
    password: yourPassword
    driver-class-name: org.postgresql.Driver

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true

  application:
    name: ecommerce-notification-service

notification:
  email:
    provider: SendGrid
    api-key: yourSendGridApiKey

  sms:
    provider: Twilio
    account-sid: yourTwilioAccountSid
    auth-token: yourTwilioAuthToken
    from-number: yourTwilioPhoneNumber

```

## Inter-Service Communication

The **E-commerce Notification Service** communicates with the following microservices:

- **[E-commerce Order Service](https://github.com/juansebstt/ecommerce-order-service)**:
    - Sends order confirmation and shipping updates after an order is placed.
- **[E-commerce Payment Service](https://github.com/juansebstt/ecommerce-payment-service):**
    - Notifies users about the status of their payments (e.g., successful, failed).
- **[E-commerce User Service](https://github.com/juansebstt/ecommerce-user-service)**:
    - Sends promotional or account-related notifications to users.
- **[E-commerce API Gateway](https://github.com/juansebstt/ecommerce-api-gateway)**
    - Routes notification-related requests from the frontend.

## Usage

### Sending a Notification

To send an email or SMS notification, make a POST request to the `/notifications/send` endpoint with the following payload:

```json
{
  "type": "email",  // or "sms"
  "recipient": "user@example.com",
  "message": "Your order has been shipped!"
}
```

### Notification Types

- **Order Confirmation**: Automatically triggered when an order is placed.
- **Payment Status**: Triggered by the Payment Service based on the success or failure of a transaction.
- **Promotions**: Can be scheduled or triggered manually to send marketing emails.

## Testing

You can use tools like **Postman** or **curl** to test the various API endpoints. Ensure proper authentication if the service is secured.

## Contributing

Feel free to submit pull requests or open issues if you find bugs or want to contribute to the project.