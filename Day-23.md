# Day 23 - PostgreSQL Database Setup for Application Deployment

## Lab Objective

The Nautilus application development team planned to deploy a new
application that requires a PostgreSQL database. The objective of this
lab was to prepare the database server by creating a dedicated database
user, creating a new database, and granting the required permissions so
the application can connect securely.

## Tasks Performed

-   Logged in to the Nautilus Database Server.
-   Switched to the PostgreSQL administrative user (`postgres`).
-   Opened the PostgreSQL interactive shell using `psql`.
-   Created a new database user:
    -   **User:** `kodekloud_sam`
    -   **Password:** `ksH85UJjhb`
-   Created a new PostgreSQL database:
    -   **Database:** `kodekloud_db5`
-   Granted all privileges on `kodekloud_db5` to the `kodekloud_sam`
    user.
-   Verified the configuration by listing database users (`\du`) and
    databases (`\l`).

## Commands Used

``` bash
sudo su - postgres
psql

CREATE USER kodekloud_sam WITH PASSWORD 'ksH85UJjhb';
CREATE DATABASE kodekloud_db5;
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db5 TO kodekloud_sam;

\du
\l
\q
```


