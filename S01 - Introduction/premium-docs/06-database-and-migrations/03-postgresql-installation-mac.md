# PostgreSQL Installation on Mac

In this lesson, I will show you how to install PostgreSQL and PG Admin on MacOS. PostgreSQL is a popular open-source relational database management system that is widely used in web development. This is what I will be using in this course but you are free to use something else like MySQL or SQLite. Laravel makes it easy to switch between databases. PG Admin is a desktop app for managing your databases.

There are a few ways to install PostgreSQL on a Mac:

1. **PostgreSQL Installer**: You can download PostgreSQL from the [official website](https://www.postgresql.org/download/).

2. **Homebrew** is a package manager for macOS that makes it easy to install and manage software.

You need to first install Homebrew if you haven't already. You can do that by running the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once you install Homebrew, you can install PostgreSQL using this command:

```bash
brew install postgresql
```

Now you have PostgreSQL installed on your Mac. You can start the PostgreSQL server using this command:

```bash
brew services start postgresql
```

If you type the following, you should see the service running:

```bash
brew services list
```

To enter the shell you can run this command:

```bash
psql postgres
```

You can run the following to list the databases:

```sql
\list
```

You should see a default database called `postgres`. You can see the users with the following command:

```sql
\du
```

You may see a user named `postgres` or you may see a user with your system user name. Remember what that username is.

## Install PG Admin

We can use the PG Admin GUI to create a new database and user.

[PG Admin](https://www.pgadmin.org/) is a graphical user interface for PostgreSQL. It makes it easy to manage your database and run queries. Even though we will be using migrations to create and manage our database, it's nice to have a GUI tool to interact with the database. You can download PG Admin from the [official website](https://www.pgadmin.org/download/).

Once you have PG Admin installed, you can move to the next lesson and we will create a new user and database for our project.

