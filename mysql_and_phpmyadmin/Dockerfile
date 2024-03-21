# Use the official MySQL image from Docker Hub
FROM mysql:latest



# Expose port 3306 to allow external connections to the MySQL server
EXPOSE 3306

# Use the official phpMyAdmin image from Docker Hub
FROM phpmyadmin/phpmyadmin:latest

# Environment variables for PHPMyAdmin
ENV PMA_HOST=mysql
ENV PMA_PORT=3306
ENV PMA_USER=my_user
ENV PMA_PASSWORD=my_password

# Expose port 80 to access phpMyAdmin web interface
EXPOSE 80