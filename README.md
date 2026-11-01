# Multi-User Expense Tracker

A full-stack multi-user expense tracking application that allows users to register, log in, manage personal expenses and categories, upload profile avatars, and view reports.

Built with **Node.js**, **Express**, **PostgreSQL**, and a vanilla HTML/CSS/JavaScript frontend.

## Features

- **User Authentication**
  - Secure registration and login
  - JWT-based authentication
  - Password hashing with bcrypt
  - Avatar upload support

- **Expense Management**
  - Create, read, update, and delete expenses
  - Assign categories and payment methods
  - Track amount, description, and date

- **Category Management**
  - Create and manage custom categories per user

- **Reports**
  - Generate expense reports and summaries

- **Frontend**
  - Clean dashboard interface
  - Static files served from the `public` directory

## Tech Stack

| Layer       | Technology                  |
|-------------|-----------------------------|
| Backend     | Node.js, Express.js         |
| Database    | PostgreSQL (`pg`)           |
| Auth        | JWT + bcryptjs              |
| File Upload | Multer                      |
| Frontend    | HTML, CSS, JavaScript       |
| Environment | dotenv                      |

## Project Structure

```
Multi-User-Expense-Tracker/
├── database/
│   └── schema.sql          # Database schema
├── public/                 # Frontend static files
│   ├── css/
│   ├── js/
│   ├── uploads/            # Uploaded avatars
│   ├── dashboard.html
│   └── index.html
├── server/
│   ├── config/
│   │   └── db.js           # PostgreSQL connection
│   ├── controllers/        # Business logic
│   ├── middleware/         # Auth & upload middleware
│   ├── routes/             # API routes
│   ├── app.js              # Express app setup
│   └── index.js            # Server entry point
├── .env                    # Environment variables
├── package.json
└── README.md
```

## Prerequisites

- Node.js (v16 or higher recommended)
- PostgreSQL
- npm or yarn

## Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/MohammadAlAmin10/Multi-User-Expense-Tracker.git
   cd Multi-User-Expense-Tracker
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**

   Create or update the `.env` file in the root directory:

   ```env
   PORT=5000
   DB_HOST=localhost
   DB_USER=postgres
   DB_PASSWORD=your_password
   DB_NAME=expense_tracker
   JWT_SECRET=your_super_secret_key
   ```

4. **Set up the database**

   - Create a PostgreSQL database named `expense_tracker` (or the name you set in `.env`).
   - Run the schema (note: the provided `schema.sql` uses MySQL-style syntax in places — adapt it for PostgreSQL if needed):

   ```bash
   psql -U postgres -d expense_tracker -f database/schema.sql
   ```

   **Recommended PostgreSQL-compatible schema adjustments:**
   - Replace `INT AUTO_INCREMENT PRIMARY KEY` with `SERIAL PRIMARY KEY`
   - Ensure all queries use PostgreSQL parameter syntax (`$1`, `$2`, etc.), which the application already does.

5. **Start the server**

   Development (with auto-reload):
   ```bash
   npm run dev
   ```

   Production:
   ```bash
   npm start
   ```

   The server will run on `http://localhost:5000` (or the port specified in `.env`).

## API Endpoints

### Authentication
| Method | Endpoint              | Description              |
|--------|-----------------------|--------------------------|
| POST   | `/api/auth/register`  | Register a new user      |
| POST   | `/api/auth/login`     | Login and receive JWT    |
| POST   | `/api/auth/avatar`    | Upload user avatar (auth required) |

### Expenses
| Method | Endpoint              | Description              |
|--------|-----------------------|--------------------------|
| *      | `/api/expenses`       | CRUD operations for expenses |

### Categories
| Method | Endpoint              | Description              |
|--------|-----------------------|--------------------------|
| *      | `/api/categories`     | Manage expense categories |

### Reports
| Method | Endpoint              | Description              |
|--------|-----------------------|--------------------------|
| *      | `/api/reports`        | Generate expense reports |

> All protected routes require a valid JWT in the `Authorization` header (`Bearer <token>`).

## Database Schema (Conceptual)

- **users** — id, name, email, password_hash, avatar_url, created_at
- **categories** — id, name, user_id
- **expenses** — id, amount, description, date, category_id, user_id, payment_method, created_at

## Scripts

| Command       | Description                     |
|---------------|---------------------------------|
| `npm start`   | Start the production server     |
| `npm run dev` | Start with nodemon (development)|

## Security Notes

- Passwords are hashed using bcrypt.
- JWT tokens expire after 7 days.
- Avatar uploads are handled via Multer and stored under `public/uploads/avatars/`.
- Never commit your real `.env` file or secrets to version control.

## License

This project is open source. Feel free to use, modify, and distribute it.

## Author

**Mohammad Al Amin**  
GitHub: [MohammadAlAmin10](https://github.com/MohammadAlAmin10)


