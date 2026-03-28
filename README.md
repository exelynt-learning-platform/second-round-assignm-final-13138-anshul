# second-round-assignm-final-13138-anshul
Final Project Assignment - This repository contains the complete final project code and documentation.
# 🛒 E-commerce Backend API

A complete Spring Boot backend for an e-commerce platform with user authentication, product management, shopping cart, order processing, and Razorpay payment integration.

## 🚀 Features

- **🔐 JWT Authentication** - Secure user registration and login
- **📦 Product Management** - CRUD operations for products
- **🛒 Shopping Cart** - Add, update, remove items
- **📋 Order Management** - Create and track orders
- **💳 Payment Integration** - Razorpay payment gateway
- **👥 Role-based Access** - Admin and User roles
- **🔄 Clean JSON Responses** - DTO-based architecture

## 📋 Prerequisites

- Java 17+
- Maven 3.6+
- MySQL 8.0+
- Razorpay Account (for payments)

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone <repository-url>
cd Ecommerce-backend
```

### 2. Database Setup
Create a MySQL database:
```sql
CREATE DATABASE ecodb;
```

### 3. Configure Application
Update `src/main/resources/application.properties`:

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/ecomdb?useSSL=false&serverTimezone=UTC
spring.datasource.username=${DB_USERNAME:your_username}
spring.datasource.password=${DB_PASSWORD:your_password}
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

# JWT Configuration
app.jwt.secret=${JWT_SECRET:your_base64_encoded_secret_key_here}
app.jwt.expiration=86400000

# Razorpay Configuration
app.razorpay.key-id=${RAZORPAY_KEY_ID:your_razorpay_key_id}
app.razorpay.key-secret=${RAZORPAY_KEY_SECRET:your_razorpay_key_secret}
```

### 4. Environment Variables Setup
Create a `.env` file for development (DO NOT commit to Git):

```bash
# Database Credentials
DB_USERNAME=your_mysql_username
DB_PASSWORD=your_mysql_password

# JWT Secret (Generate a new one for production!)
JWT_SECRET=your_base64_encoded_secret_key_here

# Razorpay Credentials
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
```

⚠️ **Security Warning**: Never commit actual credentials to version control! Use environment variables in production.

### 4. Build and Run
```bash
mvn clean install
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## 📚 API Documentation

### 🔐 Authentication

#### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
    "email": "user@example.com",
    "password": "password123"
}
```

#### Login
```http
POST /api/auth/login
Content-Type: application/json

{
    "email": "user@example.com",
    "password": "password123"
}
```

**Response:**
```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### 📦 Products

#### Get All Products
```http
GET /api/products
```

#### Get Product by ID
```http
GET /api/products/{id}
```

#### Create Product (Admin Only)
```http
POST /api/products
Authorization: Bearer ADMIN_TOKEN
Content-Type: application/json

{
    "name": "iPhone 15",
    "description": "Apple smartphone",
    "price": 80000.00,
    "stockQuantity": 10,
    "imageUrl": "https://example.com/iphone.jpg"
}
```

#### Update Product (Admin Only)
```http
PUT /api/products/{id}
Authorization: Bearer ADMIN_TOKEN
Content-Type: application/json

{
    "name": "iPhone 15 Pro",
    "price": 85000.00,
    "stockQuantity": 5
}
```

#### Delete Product (Admin Only)
```http
DELETE /api/products/{id}
Authorization: Bearer ADMIN_TOKEN
```

### 🛒 Shopping Cart

#### Get Cart Items
```http
GET /api/cart
Authorization: Bearer USER_TOKEN
```

**Response:**
```json
[
    {
        "id": 1,
        "product": {
            "id": 1,
            "name": "iPhone 15",
            "price": 80000.00
        },
        "quantity": 2,
        "totalPrice": 160000.00
    }
]
```

#### Add Item to Cart
```http
POST /api/cart/add
Authorization: Bearer USER_TOKEN
Content-Type: application/json

{
    "productId": 1,
    "quantity": 2
}
```

#### Update Cart Item
```http
PUT /api/cart/update
Authorization: Bearer USER_TOKEN
Content-Type: application/json

{
    "productId": 1,
    "quantity": 3
}
```

#### Remove Item from Cart
```http
DELETE /api/cart/{productId}
Authorization: Bearer USER_TOKEN
```

#### Clear Cart
```http
DELETE /api/cart/clear
Authorization: Bearer USER_TOKEN
```

### 📋 Orders

#### Create Order
```http
POST /api/orders/create
Authorization: Bearer USER_TOKEN
Content-Type: application/json

{
    "shippingDetails": "123 Main St, Mumbai, Maharashtra 400001"
}
```

**Response:**
```json
{
    "id": 1,
    "totalPrice": 160000.00,
    "shippingDetails": "123 Main St, Mumbai, Maharashtra 400001",
    "paymentStatus": "PENDING",
    "paymentReference": "order_1234567890",
    "createdAt": "2024-03-28T12:30:00",
    "items": [
        {
            "id": 1,
            "product": {
                "id": 1,
                "name": "iPhone 15",
                "price": 80000.00
            },
            "quantity": 2,
            "unitPrice": 80000.00
        }
    ]
}
```

#### Get User Orders
```http
GET /api/orders
Authorization: Bearer USER_TOKEN
```

#### Get Order by ID
```http
GET /api/orders/{orderId}
Authorization: Bearer USER_TOKEN
```

### 💳 Payments

#### Create Payment Order
```http
POST /api/payments/checkout
Authorization: Bearer USER_TOKEN
Content-Type: application/json

{
    "orderId": 1
}
```

**Response:**
```json
{
    "orderId": "order_1234567890",
    "checkoutUrl": null
}
```

#### Verify Payment
```http
POST /api/payments/verify
Authorization: Bearer USER_TOKEN
Content-Type: application/x-www-form-urlencoded

orderId=order_1234567890&paymentId=pay_456789&signature=abc123def456
```

**Response:**
```json
true
```

## 🔄 Complete E-commerce Flow

### 1. User Registration/Login
```bash
# Register
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'

# Login
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'
```

### 2. Add Products (Admin)
```bash
curl -X POST http://localhost:8080/api/products \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"iPhone 15","description":"Apple smartphone","price":80000.00,"stockQuantity":10}'
```

### 3. Shopping Cart Operations
```bash
# Add to cart
curl -X POST http://localhost:8080/api/cart/add \
  -H "Authorization: Bearer USER_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":1,"quantity":2}'

# View cart
curl -X GET http://localhost:8080/api/cart \
  -H "Authorization: Bearer USER_TOKEN"
```

### 4. Order Creation
```bash
curl -X POST http://localhost:8080/api/orders/create \
  -H "Authorization: Bearer USER_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"shippingDetails":"123 Main St, Mumbai, Maharashtra 400001"}'
```

### 5. Payment Processing
```bash
# Create payment order
curl -X POST http://localhost:8080/api/payments/checkout \
  -H "Authorization: Bearer USER_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"orderId":1}'

# Verify payment (after Razorpay payment)
curl -X POST http://localhost:8080/api/payments/verify \
  -H "Authorization: Bearer USER_TOKEN" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d 'orderId=order_123&paymentId=pay_456&signature=abc789'
```

## 🔒 Security Best Practices

### **Production Deployment Security**

1. **Environment Variables**
   ```bash
   # Use environment variables for all sensitive data
   export JWT_SECRET="your_secure_base64_secret"
   export DB_USERNAME="prod_db_user"
   export DB_PASSWORD="secure_db_password"
   export RAZORPAY_KEY_ID="prod_razorpay_key"
   export RAZORPAY_KEY_SECRET="prod_razorpay_secret"
   ```

2. **Generate Secure JWT Secret**
   ```bash
   # Generate a new secure secret for production
   openssl rand -base64 64
   ```

3. **Database Security**
   - Use strong passwords
   - Enable SSL connections
   - Restrict database access to application server only

4. **Admin Security**
   - Change default admin credentials immediately
   - Use strong passwords (minimum 12 characters)
   - Enable two-factor authentication if possible

5. **API Security**
   - Use HTTPS in production
   - Implement rate limiting
   - Validate all input data
   - Use CORS properly

### **Development Security**

- Never commit `.env` files to Git
- Use different credentials for development and production
- Regularly update dependencies
- Review security logs

## 🏗️ Project Structure

```
src/main/java/com/ecommerce/backend/
├── config/
│   └── DataInitializer.java
├── controller/
│   ├── AuthController.java
│   ├── CartController.java
│   ├── OrderController.java
│   ├── PaymentController.java
│   └── ProductController.java
├── dto/
│   ├── CartItemRequest.java
│   ├── CartResponse.java
│   ├── CreateOrderRequest.java
│   ├── OrderItemResponse.java
│   ├── OrderResponse.java
│   ├── PaymentRequest.java
│   ├── PaymentResponse.java
│   └── ProductResponse.java
├── exception/
│   └── GlobalExceptionHandler.java
├── model/
│   ├── CartItem.java
│   ├── CustomerOrder.java
│   ├── OrderItem.java
│   ├── PaymentStatus.java
│   ├── Product.java
│   ├── Role.java
│   └── User.java
├── repository/
│   ├── CartItemRepository.java
│   ├── CustomerOrderRepository.java
│   ├── ProductRepository.java
│   └── UserRepository.java
├── security/
│   ├── JwtAuthenticationFilter.java
│   ├── JwtService.java
│   └── SecurityConfig.java
└── service/
    ├── AuthService.java
    ├── CartService.java
    ├── OrderService.java
    └── PaymentService.java
```

## 🔧 Configuration

### Security Configuration
- JWT-based authentication
- Role-based authorization (ROLE_USER, ROLE_ADMIN)
- CSRF disabled for stateless API
- Session management disabled

### Database Configuration
- MySQL with Hibernate ORM
- Auto DDL update for development
- SQL logging enabled

### Payment Configuration
- Razorpay integration
- Order creation and verification
- Webhook support

## 🧪 Testing

### Default Admin User
The application creates a default admin user on startup:
- **Email:** admin@shop.com
- **Password:** admin123

⚠️ **Security Warning**: Change the default admin password immediately in production! Generate a secure password and update the DataInitializer.java or create users via the registration endpoint.

### Test Data
Use the provided Postman collection for testing all endpoints.

## 🐛 Troubleshooting

### Common Issues

1. **Circular Reference in JSON**
   - ✅ Fixed with DTO-based responses
   - ✅ Added @JsonIgnore annotations

2. **Cart is Empty Error**
   - Add items to cart before creating orders
   - Check product existence

3. **Payment Verification Fails**
   - Ensure Razorpay keys are correct
   - Use actual payment response values

4. **Database Connection Issues**
   - Check MySQL service is running
   - Verify credentials in application.properties

## 📝 Postman Collection

A complete Postman collection is available in the `/postman` directory:
- `Ecommerce_API_Postman_Collection.json` - API endpoints
- `Ecommerce_API_Environment.json` - Environment variables
- `README_Postman_Setup.md` - Setup instructions

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 📞 Support

For issues and questions:
- Create an issue in the repository
- Check the troubleshooting section
- Review the API documentation

---

**Built with ❤️ using Spring Boot, MySQL, and Razorpay**
