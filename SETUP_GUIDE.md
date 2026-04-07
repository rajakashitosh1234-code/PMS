# Staff Dashboard Setup Guide

## Prerequisites
You need PHP 8.1+ installed. Check if you have PHP available:

### Option 1: Find PHP Installation (Windows)
```powershell
# Search for PHP executable
Get-ChildItem "C:\Program Files" -Recurse -Name "php.exe" 2>$null
Get-ChildItem "C:\Program Files (x86)" -Recurse -Name "php.exe" 2>$null
```

### Option 2: Download PHP (if not installed)
1. Go to https://windows.php.net/download/
2. Download "VS16 x64 Thread Safe" version
3. Extract to a folder like `C:\php`
4. Add to Windows PATH:
   - Right-click "This PC" → Properties
   - Click "Advanced system settings"
   - Click "Environment Variables"
   - Click "New" under System variables
   - Variable name: `Path`
   - Variable value: `C:\php` (or wherever you extracted PHP)

---

## Setup Steps (Once PHP is in PATH)

### Step 1: Generate App Key
```powershell
cd d:\PMS\project-name
php artisan key:generate
```
Expected output: `Application key [base64:xxxx...] set successfully.`

### Step 2: Create SQLite Database File
```powershell
touch database/database.sqlite
# Or on Windows PowerShell:
New-Item -ItemType File -Path database/database.sqlite -Force
```

### Step 3: Run Migrations
```powershell
php artisan migrate
```
Expected: All migrations complete successfully

### Step 4: Seed Database
```powershell
php artisan db:seed
```
Expected: DatabaseSeeder completed successfully

### Step 5: Start Development Server
```powershell
php artisan serve
```
This starts the server at http://127.0.0.1:8000

---

## User Registration

When you first access the dashboard at `http://localhost:8000`, you'll be redirected to the login page.

**Create an account:**
1. Click **"Create new account"** link on the login page
2. Select your role: **Admin** or **Staff**
3. Fill in your details (name, email, password)
4. Click **Register**
5. You'll be redirected to login - use your new credentials

**Choose your role carefully:**
- **Admin** - Full access to all modules and settings
- **Staff** - Pharmacy staff access to medicines, sales, and inventory

---

## Dashboard Features

Once logged in, you'll have access to:

1. **Dashboard** - Sales analytics & low stock alerts
2. **Medicines** - Full inventory management
3. **Customers** - Customer records & purchase history
4. **Suppliers** - Supplier management
5. **Sales** - Create bills & manage transactions
6. **Purchases** - Purchase order management
7. **Inventory** - Stock in/out tracking
8. **Reports** - Daily, monthly, stock, and expiry reports
9. **Settings** - Profile & account preferences

---

## Troubleshooting

### PHP Not Found
→ Add PHP to PATH (see Option 1-2 above)

### SQLite Database Error
→ Ensure `database/database.sqlite` file exists and is writable

### Migration Fails
→ Check that all models are created in `app/Models/`

### Port 8000 Already in Use
```powershell
# Use a different port
php artisan serve --port=8001
```

---

## Quick Start (After Setup Complete)

```powershell
cd d:\PMS\project-name
php artisan serve
# Visit http://localhost:8000
# Login with admin@example.com / password
```
