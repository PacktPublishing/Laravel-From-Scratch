# Create a Database and User

We are going to create a database and user for our application. I am going to show you how to do this by using the PG Admin GUI tool as well as the command line.

You should have a server in PG Admin from the last lesson. Now we are going to create a new user and database.

Right click on "Login/Groups" and select "Create" and then "Login/Group Roles". I will call this login "workopia". Under the "Definition" tab, enter a password. Under the "Privileges" tab, select all of the options. This will make the user a superuser. Click on save.

Right click on "Databases" and select "Create" and then "Database". I will call this database "workopia". Under the "Definition" tab, select the owner as "workopia". Click on save.

Now you have a database and user called workopia. You could add tables and stuff from here, but we aren't going to do that. We are going to use migrations to create and manage our database.

## Using the Command Line

You can also create a database and user using the command line. Open up a terminal and type the following commands:

```bash
psql -U postgres -d postgres
```

If your default user is different than `postgres` then use that for the first instance.

Note: If you are using Windows, you may need to add the path to the `psql` executable to your system's PATH variable or you can navigate to the `C:\Program Files\PostgreSQL\16\bin` directory and run :

```bash
./psql -U postgres -d postgres
```

This will open up the PostgreSQL command line interface. You can now run the following commands:

```sql
CREATE DATABASE workopia;

CREATE USER workopia WITH SUPERUSER PASSWORD 'your_password';

GRANT ALL PRIVILEGES ON DATABASE workopia TO workopia;

-- List all databases
\l

-- List all users
\du

-- Quit
\q
```
