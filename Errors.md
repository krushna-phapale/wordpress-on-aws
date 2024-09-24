# Resolving errors encountered while configuring the project 

## Error establishing a database connection
The "Error establishing a database connection" in WordPress typically means that WordPress is unable to connect to the MySQL database. This could be due to incorrect database credentials or an issue with the MySQL server. Here's how to troubleshoot and resolve it:

## Steps to resolve

### Step 1: Check Database Credentials in wp-config.php:
Ensure the database name, username, and password are correct in the wp-config.php file.

1. Open the wp-config.php file:
```bash
   sudo nano /var/www/html/wp-config.php
```
2. Make sure the following lines have the correct information:
```php
   define( 'DB_NAME', 'wordpress' );          // Database name
    define( 'DB_USER', 'wpuser' );             // MySQL user
    define( 'DB_PASSWORD', 'your_password' );  // MySQL password
    define( 'DB_HOST', 'localhost' );          // Should be localhost if running MySQL on the same instance
```
*Double-check that the DB_NAME, DB_USER, and DB_PASSWORD match the details you created in the MySQL setup.*

### Step 2: Verify MySQL is Running:

1. Ensure that the MySQL (MariaDB) service is running:
```bash
   sudo systemctl status mariadb
```
2. If it's not running, start it:
```bash
   sudo systemctl start mariadb
```
### Step 3: Check MySQL Access:

1. Test if you can manually log in to the database using the credentials specified in wp-config.php:
```bash
   mysql -u wpuser -p
```
2. Enter the password you set for the wpuser.
3. Once logged in, ensure that the wordpress database exists by running:
```sql
   SHOW DATABASES;
```
4. If the database doesn't exist, you need to create it again:
```sql
   CREATE DATABASE wordpress;
```
5. Check that the wpuser has proper access:
```sql
   SHOW GRANTS FOR 'wpuser'@'localhost';
```
### Step 4: Check MySQL Permissions:

1. If the user doesn't have access to the wordpress database, grant the necessary permissions:
```sql
   GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
    FLUSH PRIVILEGES;
```
### Step 5: Verify Database Host:

1. Ensure DB_HOST is set to localhost in the wp-config.php. If you're using a remote database server, replace localhost with the server's IP or hostname.
### Step 6: Restart Apache and MySQL:

1. After making changes, restart both Apache and MySQL to ensure everything works properly:
```bash
   sudo systemctl restart apache2
   sudo systemctl restart mariadb
```
### Step 7: Check MySQL Connection in PHP:

1. To verify if PHP can connect to MySQL, you can create a test PHP file:
```bash
   sudo nano /var/www/html/testdb.php
```
2. Add the following content to test the connection:
```php
   <?php
    $link = mysqli_connect("localhost", "wpuser", "your_password", "wordpress");

    if (!$link) {
        die("Connection failed: " . mysqli_connect_error());
}
    echo "Connected successfully";
?>
```
3. Visit the test file by navigating to http://<your-public-ip>/testdb.php. If it says "Connected successfully", the connection is good, and the issue is likely in the wp-config.php. If not, you'll get a specific error message.
4. Don't forget to delete the test file afterward:
```bash
   sudo rm /var/www/html/testdb.php
```
