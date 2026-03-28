# 🛒 AtoZStore - E-Commerce Platform

AtoZStore is a comprehensive, fully responsive, and user-friendly e-commerce platform built by a team of four members in just two weeks. It delivers a seamless shopping experience across diverse product categories using modern technologies like **Angular**, **Spring Boot**, **MySQL**, and **Razorpay**.
Live link : https://atozstore-ecommerce-website.onrender.com
---

## 🚀 Features

### 🔑 Multi-Role Functionality

- **Customer**: Browse products, add to cart, checkout, and track orders.
- **Vendor**: Manage product listings, inventory, and orders.
- **Delivery Partner**: Access delivery schedules and update delivery statuses.
- **Admin**: Manage platform operations, users, and reports.

### 🧩 Core Functionalities

- Secure user registration and authentication.
- Dynamic product search with category filters.
- Shopping cart and streamlined checkout process.
- Razorpay integration for secure payments.
- Real-time order tracking and management for all roles.

---

## 🌟 Project Highlights

- 🧠 **Comprehensive Role Handling**: Full-stack ownership with a focus on user-centric design.
- 📱 **Responsive UI**: Optimized for mobile, tablet, and desktop devices.
- 🏗️ **Robust Architecture**: Designed with MVC and a layered pattern for maintainability.

---

## 🖥️ Frontend – Angular

### ⚙️ Key Features

#### 📦 Components

- Modularized and reusable components like: `WelcomePage`, `Home`, `Login`, `Logout`, `Products`, `OrderHistory`, `Payment`, etc.
- Effective **Parent-Child** communication for dynamic UI updates.

#### 🔄 Pipes

- Custom pipes for data transformation and enhanced UI interaction.

#### 🧭 Routing

- Implemented using `RouterModule` for seamless navigation.
- Lazy-loaded modules for improved performance.

#### 🔗 Services

- Angular Services (with **Axios**) for API interaction and business logic handling.

#### 📱 Responsive Design

- Layouts compatible with all device sizes.
- Used Bootstrap & Angular Material for UI design and responsiveness.

#### 📁 Assets Directory

- Contains images and static assets used in the UI.

#### 📌 Module.ts

- Acts as the metadata hub; registers components, modules, and services.

### 🛠️ Tools & Technologies

- Angular
- TypeScript
- CSS/SCSS
- Axios
- Bootstrap / Angular Material
- Visual Studio Code
- Git & GitHub

---

## 🔧 Backend – Spring Boot

### 🏗️ Architecture & Request Flow

1. Frontend sends request → `Controller`
2. Controller maps data to POJOs → Passes to `Service` layer
3. Service layer handles core logic → Interacts with `DAO`
4. DAO (via **JPA**) performs DB operations
5. Response flows back to frontend

### 📂 Resources Directory

- Contains static resources and configuration (`application.properties`).

### 📧 Email Feature

- Integrated Java Mail API for automated email sending.

### 💳 Payment Integration

- **Razorpay API** integrated for secure online payments.

### 🌟 Key Backend Features

- Layered architecture for clean separation of concerns.
- Spring annotations for dependency injection and configuration.
- `pom.xml` for Maven-based dependency management.

### 🗃️ Database

- **MySQL** for data persistence.
- **JPA** for Object-Relational Mapping (ORM).

### 🛠️ Tools & Technologies

- Spring Boot
- Java
- JPA (Hibernate)
- Razorpay API
- Maven
- Spring Tool Suite (STS)
- Git & GitHub

---

## 📌 Conclusion

**AtoZStore** is a scalable and robust full-stack e-commerce solution with multi-role functionality, responsive design, and seamless third-party integrations. It reflects strong teamwork, sound architecture, and a keen focus on usability.

---
