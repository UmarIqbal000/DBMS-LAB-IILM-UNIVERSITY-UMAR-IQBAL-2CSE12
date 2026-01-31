# 🗄️ How to Access SQL (MySQL/MariaDB)

> A step-by-step guide to access MySQL/MariaDB database using XAMPP on Windows and macOS.

---

## 📋 Prerequisites

- **XAMPP** installed on your system
- MySQL/MariaDB service running

---

## 💻 Windows Users

### Step 1: Start XAMPP Services

1. Open **XAMPP Control Panel**
2. Click **Start** next to **Apache** (optional, for phpMyAdmin)
3. Click **Start** next to **MySQL**
4. Wait until both show green "Running" status

### Step 2: Open Command Prompt

Press `Win + R`, type `cmd`, and press Enter.

### Step 3: Navigate to MySQL Bin Directory

```bash
cd C:\xampp\mysql\bin
```

### Step 4: Connect to MySQL

#### Option A: Default Login (No Password)

```bash
mysql -u root
```

#### Option B: Login with Password

```bash
mysql -u root -p
```

> 💡 **Note:** After entering this command, you'll be prompted to enter your password. Press Enter if no password is set.

### Step 5: Successful Connection

You should see output similar to:

```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.4.32-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

---

## 🍎 macOS Users

### Step 1: Install XAMPP

1. Download XAMPP for macOS from [apachefriends.org](https://www.apachefriends.org/)
2. Open the `.dmg` file and drag XAMPP to Applications
3. Go to **System Preferences → Security & Privacy → General**
4. Click **Allow** to give XAMPP necessary permissions

### Step 2: Start XAMPP Services

1. Open **XAMPP** from Applications folder
2. Open **XAMPP Control Panel**
3. Go to **Manage Servers** tab
4. Select **Apache Web Server** → Click **Start**
5. Select **MySQL Database** → Click **Start**
6. Both should show status as **Running** ✅

### Step 3: Open Terminal

Press `Cmd + Space`, type `Terminal`, and press Enter.

### Step 4: Connect to MySQL

```bash
/Applications/XAMPP/xamppfiles/bin/mysql -u root
```

#### With Password

```bash
/Applications/XAMPP/xamppfiles/bin/mysql -u root -p
```

### Step 5: Successful Connection

You should see the MariaDB welcome message as shown above.

---

## 🔧 Useful MySQL Commands

| Command | Description |
|---------|-------------|
| `SHOW DATABASES;` | List all databases |
| `USE database_name;` | Select a database |
| `SHOW TABLES;` | List tables in current database |
| `DESCRIBE table_name;` | Show table structure |
| `EXIT;` or `\q` | Exit MySQL prompt |

---

## 🆘 Troubleshooting

### Error: 'mysql' is not recognized (Windows)

**Solution:** You're not in the correct directory. Run:
```bash
cd C:\xampp\mysql\bin
```

### Error: Access denied for user 'root'

**Solution:** Use the password flag:
```bash
mysql -u root -p
```

### Error: Can't connect to MySQL server

**Solution:** 
1. Open XAMPP Control Panel
2. Make sure MySQL is **Running** (green)
3. If not, click **Start** next to MySQL

### Port 3306 Already in Use

**Solution:**
1. Open XAMPP Control Panel
2. Click **Config** next to MySQL
3. Change port from `3306` to `3307`
4. Update connection command:
```bash
mysql -u root -P 3307
```

---

## 📌 Quick Reference

### Windows Quick Start
```bash
cd C:\xampp\mysql\bin
mysql -u root
```

### macOS Quick Start
```bash
/Applications/XAMPP/xamppfiles/bin/mysql -u root
```

---

> **Tip:** Create a desktop shortcut or alias for faster access in future sessions!

---

**Happy Querying! 🚀**
