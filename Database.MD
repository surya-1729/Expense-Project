## MySQL Database Installation & Setup: Expense Project

### 1. Install MySQL Server 8.0.x
Install the MySQL server package using DNF:
```bash
dnf install mysql-server -y
```

***

### 2. Enable and Start MySQL Service
Make MySQL start automatically at boot and start the service immediately:
```bash
systemctl enable mysqld
systemctl start mysqld
```

***

### 3. Secure MySQL Installation and Set Root Password
Run the security script to configure basic MySQL security settings and set a new root password (`ExpenseApp@1` or any other password you choose):
```bash
mysql_secure_installation --set-root-pass ExpenseApp@1
```

***

### 4. Verification and Basic MySQL Commands

- **Connect to MySQL server:**
  If MySQL server and client are on the same host, use:
  ```bash
  mysql
  ```
  Otherwise, specify host, user, and password:
  ```bash
  mysql -h <host-address> -u root -p<password>
  ```
- **Show available databases:**
  ```sql
  show databases;
  ```
- **Use a specific database (schema):**
  ```sql
  use <database_name>;
  ```
- **List tables in the current database:**
  ```sql
  show tables;
  ```
- **Query data from a table:**
  ```sql
  select * from <table_name>;
  ```

***

### Summary
- Installing and enabling MySQL server ensures the database service runs reliably.
- Changing the root password secures the database.
- Using basic MySQL commands helps to validate and interact with your databases.

This setup enables your backend application to connect and use MySQL securely and effectively.

***

If any customization or troubleshooting is needed, check MySQL logs or configuration files located typically under `/var/log/mysqld.log` and `/etc/my.cnf`.