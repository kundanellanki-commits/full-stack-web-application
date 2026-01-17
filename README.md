# full-stack-web-application
A full-stack web application that allows users to submit and manage ratings for registered stores using a secure role-based login system. It supports Admin, Normal User, and Store Owner roles with dedicated dashboards. Built using React.js, Node.js (Express), and an SQL database following best practices.
## Tech Stack
- **Backend**: NestJS with TypeScript
- **Database**: PostgreSQL
- **Frontend**: React with TypeScript

## Project Structure
```
├── backend/          # NestJS backend application
│   ├── src/
│   │   ├── auth/     # Authentication module
│   │   ├── users/    # User management module
│   │   ├── stores/   # Store management module
│   │   ├── ratings/  # Rating management module
│   │   └── entities/ # Database entities
├── frontend/         # React frontend application
│   ├── src/
│   │   ├── pages/    # Page components
│   │   ├── components/ # Reusable components
│   │   └── context/  # React context (Auth)
└── README.md
```

## Setup Instructions

### Prerequisites
- Node.js (v16 or higher)
- PostgreSQL (v12 or higher)
- npm or yarn

### Database Setup
1. Create a PostgreSQL database:
```sql
CREATE DATABASE store_rating_db;
```

### Backend Setup
1. Navigate to backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file in the backend directory:
```env
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_DATABASE=store_rating_db

JWT_SECRET=your-super-secret-jwt-key-change-in-production
JWT_EXPIRES_IN=7d

PORT=3000
```

4. Start the backend server:
```bash
npm run start:dev
```

The backend will run on `http://localhost:3000`

### Frontend Setup
1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the frontend development server:
```bash
npm start
```

The frontend will run on `http://localhost:3001` (or 3000 if 3001 is unavailable)

## Features

### System Administrator
- Dashboard with statistics (total users, stores, ratings)
- Add new stores, normal users, and admin users
- View and filter lists of users and stores
- Sort tables by Name, Email, Address, Role
- View detailed user information
- Change password

### Normal User
- Sign up and login
- View all registered stores
- Search stores by Name and Address
- Submit ratings (1-5) for stores
- Modify submitted ratings
- See overall rating and user's submitted rating for each store
- Change password

### Store Owner
- Dashboard showing users who rated their store
- View average rating of their store
- Change password

## API Endpoints

### Authentication
- `POST /auth/login` - User login
- `POST /auth/register` - User registration
- `PUT /auth/password` - Update password (authenticated)

### Users (Admin only)
- `GET /users/dashboard` - Get dashboard statistics
- `GET /users` - Get all users with filters
- `POST /users` - Create new user
- `GET /users/:id` - Get user details

### Stores
- `GET /stores` - Get all stores (with filters for admin, search for users)
- `POST /stores` - Create store (admin only)
- `GET /stores/dashboard` - Get store owner dashboard (store owner only)
- `GET /stores/:id` - Get store details

### Ratings (Normal users only)
- `POST /ratings` - Submit or update rating
- `GET /ratings` - Get user's ratings
- `GET /ratings/:id` - Get rating details
- `DELETE /ratings/:id` - Delete rating

## Form Validations

- **Name**: Minimum 20 characters, Maximum 60 characters
- **Email**: Standard email validation
- **Address**: Maximum 400 characters
- **Password**: 8-16 characters, must include at least one uppercase letter and one special character

## Database Schema

- **Users**: id, name, email, password, address, role, createdAt, updatedAt
- **Stores**: id, name, email, address, ownerId, createdAt, updatedAt
- **Ratings**: id, rating (1-5), userId, storeId, createdAt, updatedAt

## Notes

- All authenticated endpoints require JWT token in Authorization header
- Role-based access control is enforced on all endpoints
- Database relationships ensure data integrity
- Frontend and backend validations are implemented

