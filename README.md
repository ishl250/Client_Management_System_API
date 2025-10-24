# Client_Management_System_API

# 🚀 express-mysql-jwt-auth-api

A secure and extensible **Client Management System API** built with **Express**, **MySQL2**, **JWT**, and **bcryptjs**.  
This project provides a complete backend for user registration, authentication, authorization, and transaction tracking.

---

## 🧰 Tech Stack

- **Node.js** (Express Framework)
- **MySQL2** (Database)
- **bcryptjs** (Password hashing)
- **jsonwebtoken (JWT)** (Authentication)
- **CORS**
- **dotenv** (Environment variables)

---

## 📦 Features

✅ User registration and login  
✅ JWT-based authentication  
✅ Role-based access control (admin & user)  
✅ CRUD operations for users  
✅ Transaction management (linked to users)  
✅ Paginated user listing  
✅ Password encryption  
✅ Error handling & 404 fallback routes  

---

## ⚙️ Installation & Setup

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/<your-username>/Client_Management_System_API.git
cd Client_Management_System_API
````

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Setup Environment Variables

Create a `.env` file in the project root and add the following:

```env
PORT=2500
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASS=123
DB_NAME=l4sod
JWT_SECRET=jhdfvsdfgcdjwtssfsf
```

### 4️⃣ Start the Server

```bash
npm start
```

Server will start at:
👉 `http://localhost:2500`

---

## 🗃️ Database Schema

### **Users Table**

```sql
CREATE TABLE users (
  user_id INT AUTO_INCREMENT PRIMARY KEY,
  user_name VARCHAR(255),
  Email VARCHAR(255) UNIQUE,
  password VARCHAR(255),
  role ENUM('user', 'admin') DEFAULT 'user',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### **Transactions Table**

```sql
CREATE TABLE transactions (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  amount DECIMAL(10,2),
  status ENUM('pending','completed') DEFAULT 'pending',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

---

## 🧱 API Endpoints

| Method | Endpoint                  | Description                           | Auth | Admin |
| :----: | :------------------------ | :------------------------------------ | :--: | :---: |
|   GET  | `/`                       | Welcome message                       |   ❌  |   ❌   |
|  POST  | `/users`                  | Register a new user                   |   ❌  |   ❌   |
|   GET  | `/users`                  | Get all users (paginated)             |   ✅  |   ✅   |
|   GET  | `/users/:user_id`         | Get user by ID                        |   ❌  |   ❌   |
|   PUT  | `/users/:user_id`         | Update user details                   |   ❌  |   ❌   |
| DELETE | `/users/:user_id`         | Delete user                           |   ❌  |   ❌   |
|  POST  | `/login`                  | User login & JWT token                |   ❌  |   ❌   |
|  POST  | `/create-transaction`     | Create transaction for logged-in user |   ✅  |   ❌   |
|   GET  | `/users-with-transactios` | Get users with transactions           |   ❌  |   ❌   |

✅ = Requires JWT
❌ = Public access

---

## 🔐 Authentication

### Login Example

```json
POST /login
{
  "email": "user@example.com",
  "password": "yourpassword"
}
```

Response:

```json
{
  "user": {
    "user_id": 1,
    "user_name": "John Doe",
    "Email": "user@example.com",
    "role": "user"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5..."
}
```

Use the token for protected routes:

```
Authorization: Bearer <token>
```

---

## 🧪 Example Admin Flow

1️⃣ Create an admin manually in the database:

```sql
INSERT INTO users (user_name, Email, password, role)
VALUES ('Admin', 'admin@example.com', '<hashed_password>', 'admin');
```

2️⃣ Login with the admin credentials to receive a token.
3️⃣ Call protected routes like `/users` with:

```
Authorization: Bearer <token>
```

---

## 🧰 Development Scripts

| Command       | Description                       |
| ------------- | --------------------------------- |
| `npm start`   | Run the server                    |
| `npm run dev` | Run with Nodemon (optional setup) |

---

## 🧱 Folder Structure

```
Client_Management_System_API/
├── server.js
├── package.json
├── .env
└── README.md
```

*(You can later modularize into routes, controllers, and middleware folders.)*

---

## 📜 License

MIT License © 2025 [ishl250](https://github.com/ishl250)

---

## 💬 Author

Built with ❤️ by **[ishimwejeanclaude](https://github.com/ishl250/ishimwejeanclaude)**
Contributions, issues, and pull requests are always welcome!



