# Day 24 – Install and Configure MariaDB Database Server

## Objective
Install and configure MariaDB on the Nautilus DB Server, create a new database, create a database user, and grant the required privileges.

---

## Task Requirements

- Install and configure MariaDB Server.
- Create a database named **kodekloud_db5**.
- Create a user **kodekloud_joy** with password **TmPcZjtRQx**.
- Grant full privileges on **kodekloud_db5** to **kodekloud_joy**.

---

## Steps Performed

### 1. Install MariaDB Server

```bash
sudo yum install -y mariadb-server
```

### 2. Start and Enable the MariaDB Service

```bash
sudo systemctl enable mariadb
sudo systemctl start mariadb
```

### 3. Verify the Service Status

```bash
sudo systemctl status mariadb
```

### 4. Access the MariaDB Shell

```bash
sudo mysql
```

### 5. Create the Database

```sql
CREATE DATABASE kodekloud_db5;
```

### 6. Create a New Database User

```sql
CREATE USER 'kodekloud_joy'@'localhost' IDENTIFIED BY 'TmPcZjtRQx';
```

### 7. Grant Full Privileges

```sql
GRANT ALL PRIVILEGES ON kodekloud_db5.* TO 'kodekloud_joy'@'localhost';
FLUSH PRIVILEGES;
```

### 8. Verify the Configuration

```sql
SHOW DATABASES;
SHOW GRANTS FOR 'kodekloud_joy'@'localhost';
EXIT;
```

---

## Outcome

- MariaDB Server installed and running successfully.
- Database **kodekloud_db5** created.
- User **kodekloud_joy** created with the specified password.
- Full privileges granted on **kodekloud_db5**.
- Database setup completed successfully.

---

## Skills Practiced

- MariaDB Installation
- Database Creation
- User Management
- Permission Management (GRANT)
- MariaDB Service Management
- Linux Database Administration