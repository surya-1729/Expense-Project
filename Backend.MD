## Backend Service Deployment: Expense Application

### 1. Install NodeJS (Version 20+)
Ensure you install NodeJS version 20 or above as required by your developer.

- **List available NodeJS modules:**
  ```bash
  dnf module list nodejs
  ```

- **Switch NodeJS module to version 20:**
  ```bash
  dnf module disable nodejs -y
  dnf module enable nodejs:20 -y
  dnf install nodejs -y
  ```

***

### 2. Prepare Application Environment

- **Create dedicated application user (not for interactive login):**
  ```bash
  useradd expense
  ```

- **Set up standard app directory:**
  ```bash
  mkdir /app
  ```

***

### 3. Deploy Backend Code

- **Download and extract the backend code:**
  ```bash
  curl -o /tmp/backend.zip https://expense-builds.s3.us-east-1.amazonaws.com/expense-backend-v2.zip
  cd /app
  unzip /tmp/backend.zip
  ```

- **Install application dependencies:**
  ```bash
  cd /app
  npm install
  ```

***

### 4. Configure systemd for Backend Service

- **Create the systemd service file:**
  ```bash
  vim /etc/systemd/system/backend.service
  ```
  Add the following content (replace `<MYSQL-SERVER-IPADDRESS>` with your MySQL host IP):

  ```
  [Unit]
  Description=Backend Service

  [Service]
  User=expense
  Environment=DB_HOST="<MYSQL-SERVER-IPADDRESS>"
  ExecStart=/bin/node /app/index.js
  SyslogIdentifier=backend

  [Install]
  WantedBy=multi-user.target
  ```

***

### 5. Start and Enable Backend Service

- **Reload systemd and start the backend:**
  ```bash
  systemctl daemon-reload
  systemctl start backend
  systemctl enable backend
  ```

***

### 6. Load Database Schema

- **Install MySQL client (if not already present):**
  ```bash
  dnf install mysql -y
  ```

- **Load schema to the database:**
  ```bash
  mysql -h <MYSQL-SERVER-IPADDRESS> -uroot -pExpenseApp@1 < /app/schema/backend.sql
  ```

***

### 7. Finalize

- **Restart backend to ensure all changes take effect:**
  ```bash
  systemctl restart backend
  ```

***

**You have now set up the Expense backend service with proper NodeJS version, code deployment, systemd integration, and database initialization.**