# AWS Server Troubleshooting Guide

This guide helps verify if an AWS server is performing according to its configuration by checking critical processes, network connections, and services.  

***

### 1. Check Active Network Listening Ports

Run:

```bash
netstat -lntp
```

- Confirms which ports are listening and which processes own them.  
- Ensure expected services are active, for example:  
  - Nginx on **80/443**  
  - MySQL on **3306**  
  - Custom backend application ports  
- Verify no unexpected ports or rogue processes are open.  

***

### 2. Verify Critical Processes Are Running

Run:

```bash
ps -ef | grep <process-name>
```

- Replace `<process-name>` with the service to verify (e.g., `nginx`, `mysqld`, `node`).  
- Confirms the process is active and shows the parent process or launch user.  
- If not found, the service may be **down** or **failed to start**.  

