# 📦 Minimal E-Commerce System (Backend)

This project is a functional implementation of an E-commerce backend service. It demonstrates key backend concepts such as REST API design, NoSQL data modeling with MongoDB, and Event-Driven architecture using Webhooks.

## 🎯 Project Objectives
The system was built to solve three main challenges:
1.  **Data Integrity:** Managing relationships between Users, Products, and Orders in a NoSQL database.
2.  **Concurrency:** Handling stock deduction safely when an order is placed.
3.  **Asynchronous Events:** Simulating a real-world payment gateway (like Razorpay) that confirms payments after a delay.

## 🏗️ Architecture
* **Controller Layer:** Exposes REST endpoints.
* **Service Layer:** Contains business logic (e.g., preventing ordering out-of-stock items).
* **Repository Layer:** Communicates with MongoDB Atlas.
* **Webhook Listener:** A dedicated endpoint that listens for payment success events.

## 💻 How to Run

### Prerequisites
* Java JDK 17 or higher
* Maven
* MongoDB Atlas Account

### Configuration Steps
1.  Navigate to `src/main/resources/application.properties`.
2.  Update the database configuration:
    ```properties
    spring.application.name=ecommerce
    server.port=8080
    spring.data.mongodb.uri=YOUR_CONNECTION_STRING_HERE
    spring.data.mongodb.database=ecommerce_db
    ```
3.  Start the application via your IDE or terminal: `mvn spring-boot:run`

## 🧪 Testing the Flow (Postman)

**Step 1: Browse & Shop**
* Create products using `POST /api/products`.
* Add them to your cart using `POST /api/cart/add`.

**Step 2: Checkout**
* Send `POST /api/orders` with your `userId`.
* *Result:* Order is created with status `CREATED`. Stock is automatically deducted.

**Step 3: Payment Simulation**
* Send `POST /api/payments/create` with the `orderId`.
* *Response:* You will get a `PENDING` status immediately.
* **Wait 3 Seconds...** The system simulates bank processing in the background.
* Check the order status again (`GET /api/orders/{id}`). It will now be `PAID`.

    ## Made By- Chhavi 😁
