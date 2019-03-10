# Connecting to a Remote MySQL Database using an SSH tunnel, and Python.
This tutorial will show you how to connect to a remote machine hosting a MySQL database; the connection will
be made using an SSH Tunnel. We will then query the database using Python's pymysql library .

## STEP 1: From the command line, create an SSH tunnel to machine with your database:
From the command line, you will need to create a connection to the server that is running the database.
Most standard MySQL instances are run on port 3306. If the MySQL instance on your server is running on a
Different port, you may need to change that number.

    ssh -i key.pem -fN -L 3307:localhost:3306 username@site_or_ip_address_hosting_the_database

Next, we will install python's pymysql package

    pip install PyMySQL


## STEP 2: Query the database from Python.
from python, run the following script, and you should be all set.

    import pymysql
    cnx = pymysql.connect(db     = 'database_name', 
                      user   = 'database_username', 
                      passwd = 'database_password', 
                      host   = '127.0.0.1', 
                      port   = 3307,
                      ) 
    cursor = cnx.cursor()
    cursor.execute("SELECT NOW()")
    result = cursor.fetchall()
    cursor.close()
    cnx.close()

    print(result)
