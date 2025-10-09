# Handle MailCrux Database

## Step 1 : Login into Server
```bash
ssh root@username-p 22
password
```
replace Your Username and password

## Step 2: Go to Docker Container
```bash
docker exec -it {container-name} bash
```

Example - 
```bash
docker exec -it postal-mariadb bash
```

## Step 3: Goto MariaDB 
```bash
mariadb -u root -p
use mailcrux
```

## step 4: data base commands
```bash
show tables;
select * from servers where name="domain name"

