# 🚀 Docker Setup and Postal Service Check Guide
## Step 1: Login to the Server

Connect to the server using SSH key authentication.

When prompted, enter the password.

```bash
ssh user@your_server_ip
```

## Step 2: Verify Running Docker Containers

Check if there are any active Docker containers:
```bash
docker ps
```

This command lists all currently running containers.

## Step 3: Start Postal Service

Start the Postal service with 10 worker instances:

```bash
postal start --scale worker=10
````

## Step 4: Recheck Running Containers

After starting Postal, confirm that the containers are running:
```bash
docker ps
```

You should see multiple containers including the Postal workers.

## Step 5: Check Postal Worker Logs

View the latest 50 lines of logs from the Postal worker container:

```bash
docker logs postal_worker_1 --tail=50
```

If you see a message similar to:

```bash
INFO Joined outgoing
```

## ✅ It means the Postal worker is running successfully!
