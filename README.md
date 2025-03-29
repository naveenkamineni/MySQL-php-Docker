# MySQL + PHP + Docker

This guide explains how to set up and run MySQL and phpMyAdmin using Docker, allowing you to manage MySQL databases through a web interface.

---

## 🚀 Step 1: Pull MySQL Image from Docker Hub
First, download the latest MySQL image:
```bash
docker image pull mysql:latest
```

## 🐳 Step 2: Run MySQL Container
Start a MySQL container with user authentication:
```bash
docker run -itd --name mysql-con1 -p 3307:3306 \
-e MYSQL_ROOT_PASSWORD=rootpassword \
-e MYSQL_USER=nave \
-e MYSQL_PASSWORD=pass \
mysql:latest
```
This command:
- Runs MySQL in detached mode (`-itd`).
- Names the container `mysql-con1`.
- Maps MySQL's internal port `3306` to `3307` on your machine.
- Sets up MySQL with a root password and a user (`nave`).

To check if MySQL is running, you can use:
```bash
netstat -tulnp | grep 3306
```

---

## 🌐 Step 3: Run phpMyAdmin
Now, set up phpMyAdmin to interact with MySQL through a web browser:
```bash
docker run -itd --name phpmyadmin -p 8080:80 \
--link mysql-con1:db \
-e PMA_HOST=mysql-con1 \
phpmyadmin/phpmyadmin
```
This command:
- Runs phpMyAdmin in detached mode.
- Names the container `phpmyadmin`.
- Maps port `80` inside the container to `8080` on your host machine.
- Links phpMyAdmin to the `mysql-con1` container.

---

## 🔗 Step 4: Access phpMyAdmin on Your Web Browser
Once phpMyAdmin is running, access it through your browser:
```
http://<EC2-Public-IP>:8080
```
Use the following credentials to log in:
- **Username:** `root`
- **Password:** `rootpassword`

---

## 🛑 Stopping and Removing Containers
To stop MySQL and phpMyAdmin containers:
```bash
docker stop mysql-con1 phpmyadmin
```
To remove the containers:
```bash
docker rm mysql-con1 phpmyadmin
```

---

## 🎯 Conclusion
By following this guide, you have successfully set up MySQL and phpMyAdmin using Docker. You can now manage your databases easily via a web browser.

📌 **Happy Coding!** 🚀


