# MailCrux Database Management Guide

This document outlines the steps to manage and interact with the MailCrux database using Docker and MariaDB.

## Prerequisites

- SSH access to the server.
- A running Docker container with MariaDB.
- MariaDB root credentials.

## Step 1: Log in to the Server

SSH into the server using the following command:

```bash
ssh root@username -p 22
```
docker exec -it {container-name} bash
Replace {container-name} with the actual name of the container.

Example: If you're using the postal-mariadb container, run:

```bash
docker exec -it postal-mariadb bash
```
Step 3: Access MariaDB
Inside the Docker container, connect to MariaDB by running the following:

```bash
mariadb -u root -p
```
You'll be prompted for the MariaDB root password.

Once logged in, switch to the mailcrux database:

```bash
use mailcrux;
```
Step 4: Run Database Commands
1. Show Tables
To list all tables in the mailcrux database:

```bash
show tables;
```
2. Search for a Specific Server by Domain Name
To query a specific server by domain name:

```bash
select * from servers where name="your-domain-name";
```
Replace your-domain-name with the actual domain you’re searching for.

3. Switch to a Specific Server's Database
To switch to a specific server’s database, use its server ID:

```bash
use mailcrux-server-{server-id};
```
Replace {server-id} with the actual server ID.

4. Count "Hard Fail" Messages
To count the number of "hardfail" messages:

```bash
select count(*) from messages where status="hardfail";
```
5. Delete "Hard Fail" Messages
To delete all "hardfail" messages:

```bash
delete from messages where status="hardfail";
```
6. Delete Suppressions
To delete all suppressed email addresses:

```bash
delete from suppressions;
```

7. Reset Bounce Stats
To reset the daily bounce statistics:

```bash
update stats daily set bouces=0;
```
8. Count "Held" Messages
To count the number of messages that are "held":

```bash
select count(*) from messages where status="held";
```
Step 5: Exit the Database and Docker Container
After completing your database operations, exit MariaDB and the Docker container:

Exit MariaDB:

```bash
\q
```
Exit the Docker container:

```bash
exit
```
Finally, exit the SSH session:

```bash
exit
```
