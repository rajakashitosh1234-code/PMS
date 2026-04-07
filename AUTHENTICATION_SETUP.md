# Role-Based Authentication Setup

## Changes Made

### 1. ✅ Updated Setup Guide
- Removed hardcoded login credentials
- Added instructions for user registration
- Explained Admin vs Staff roles

### 2. ✅ Login Page Enhanced
- **File:** `resources/views/auth/login.blade.php`
- Added "Create new account" button with registration link
- Removed demo credentials note
- Now links to `/register` route

### 3. ✅ Registration Page Created
- **File:** `resources/views/auth/register.blade.php`
- Role selection dropdown (Admin / Staff)
- Form fields:
  - Full Name
  - Email Address (unique)
  - Phone Number (unique)
  - Role (Admin or Staff)
  - Password (min 8 chars)
  - Confirm Password
- Success redirect to login page

### 4. ✅ AuthController Updated
- **File:** `app/Http/Controllers/AuthController.php`
- Added `showLogin()` method
- Added `showRegister()` method  
- Added `register()` method with validation:
  - Unique email & phone checks
  - Password confirmation
  - Role-based user creation

### 5. ✅ Routes Updated
- **File:** `routes/web.php`
- Public routes (guest middleware):
  - `GET /login` → `showLogin()`
  - `POST /login` → `login()`
  - `GET /register` → `showRegister()`
  - `POST /register` → `register()`
- Protected routes:
  - `POST /logout` → `logout()` (auth required)

### 6. ✅ Middleware Updated
- **File:** `app/Http/Middleware/Authenticate.php`
- Redirects unauthenticated users to `auth.login` route

### 7. ✅ Database Seeder Updated
- **File:** `database/seeders/DatabaseSeeder.php`
- Removed hardcoded user creation
- Users now created through registration page
- Kept sample medicines, customers, suppliers

---

## How It Works

### First Time User
```
1. Visit http://localhost:8000
2. Redirected to login page
3. Click "Create new account"
4. Fill registration form with role selection
5. Choose Admin or Staff role
6. System creates account and redirects to login
7. Login with credentials
```

### Admin vs Staff Roles

**Admin Role:**
- Full access to all dashboard features
- Can manage all medicines, sales, customers, suppliers
- Can view all reports
- Can access settings

**Staff Role:**
- Pharmacy staff focused permissions
- Can process sales/bills
- Can check inventory
- Can view limited reports
- Limited settings access

---

## Setup Instructions (After PHP Install)

```powershell
cd d:\PMS\project-name

# 1. Generate app key
php artisan key:generate

# 2. Create SQLite database
New-Item -ItemType File -Path database/database.sqlite -Force

# 3. Run migrations
php artisan migrate

# 4. Seed sample data (medicines, customers, suppliers)
php artisan db:seed

# 5. Start development server
php artisan serve

# 6. Open in browser
# http://localhost:8000 → Redirects to login
# Click "Create new account"
# Register as Admin or Staff
# Login and access dashboard
```

---

## Key Features

✅ **Registration with Role Selection**
- Admin and Staff roles
- Email/Phone validation
- Unique constraint enforcement
- Password confirmation

✅ **Secure Authentication**
- Password hashing (automatic)
- Session management
- Guest middleware for public routes
- Auth middleware for protected routes

✅ **User-Friendly Flow**
- From login page, users can register
- Registration redirects to login
- Clear success messages
- Error handling for validation

✅ **Database Ready**
- Users table configured for roles
- Sample data includes medicines, customers, suppliers
- Ready for transactions (sales, purchases)

---

## Testing the System

1. **First Registration:**
   - Register as Admin - get full access
   - Register as Staff - get staff-only access

2. **Login:**
   - Use registered email and password
   - Dashboard loads based on role permissions

3. **Sample Data:**
   - 8 medicines available after seeding
   - 3 customers and 2 suppliers pre-populated
   - Ready for sales transactions

---

## Files Modified

- ✅ `SETUP_GUIDE.md` - Updated with registration instructions
- ✅ `resources/views/auth/login.blade.php` - Added register link
- ✅ `resources/views/auth/register.blade.php` - NEW: Registration form
- ✅ `app/Http/Controllers/AuthController.php` - Added register methods
- ✅ `routes/web.php` - Added registration routes + guest middleware
- ✅ `app/Http/Middleware/Authenticate.php` - Updated redirect route
- ✅ `database/seeders/DatabaseSeeder.php` - Removed hardcoded users

---

## Next Steps

1. Install PHP and add to PATH
2. Run migrations and seeding
3. Access http://localhost:8000
4. Register first account as Admin
5. Register additional Staff accounts as needed
6. Use dashboard to manage pharmacy operations
