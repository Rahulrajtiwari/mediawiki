# Use the official MySQL image as a base
FROM mysql:5.7

# Set environment variables for the database name, user, and password
ENV MYSQL_DATABASE=wiki_db
ENV MYSQL_USER=wikimedia
ENV MYSQL_PASSWORD=wikimedia
ENV MYSQL_RANDOM_ROOT_PASSWORD=yes

# Set the initial SQL commands to be executed on startup
ENV MYSQL_INIT_FILE=/docker-entrypoint-initdb.d/init.sql

# Create the init.sql file with the necessary SQL commands
COPY init.sql /docker-entrypoint-initdb.d/


# Expose the MySQL port
EXPOSE 3306

# The command to run when the container starts
CMD ["mysqld"]
