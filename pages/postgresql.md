<div align='center'>

# Postgre SQL
</div>

## Installation

```bash
cd Downloads/
```

Create File 

```bash
touch install-postgresql.sh
```

open the file with txt file and copy-paste the bellow code - 

```bash
sudo apt install curl ca-certificates
sudo install -d /usr/share/postgresql-common/pgdg
sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
. /etc/os-release
sudo sh -c "echo 'deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $VERSION_CODENAME-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
sudo apt update
sudo apt -y install postgresql
```

Make the code execute :
```bash
chmod +x install-postgresql.sh
```

After saved then back to the terminal and run that command :
```bash
./install-postgresql.sh
```

## Use

goto postgres terminal
```bash
sudo -i -u postgres
```

your terminal look like : `postgres@hp-elitebook-840-g4:~$`


then connect with postgre serve just type
```bash
psql
```

- Now you can access database and your terminal look like start

```bash
postgres=#
```

- Create Database 

```bash
CREATE DATABASE my_database;
```

Check database created or not : by typing `\l` 
```bash
postgres=# \l
```
 press `q` to exit and back to  `postgres=#`

 - To connected Database by `\c my_database`

 ```bash
postgres=# \c my_database
 ```

Now your terminal look like start

```bash
my_database-#
```

- Now If you want to quit just write - 
`\q`.
```bash
my_database-# \q
```

return back to `postgres@hp-elitebook-840-g4:~$`

## GUI (pgAdmin)

Open terminal and just follow the command given below

```bash
#
# Setup the repository
#

# Install the public key for the repository (if not done previously):
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

# Create the repository configuration file:
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

#
# Install pgAdmin
#

# Install for both desktop and web modes:
sudo apt install pgadmin4

# Install for desktop mode only:
sudo apt install pgadmin4-desktop

# Install for web mode only: 
sudo apt install pgadmin4-web 

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh
```

### Alternative : 
goto Downlaod Folder or others and create this file : 

```bash
touch install-pgadmin.sh
```

To executable :
```bash
chmod +x install-pgadmin.sh
```

Install just type : 
```bash
./install-pgadmin.sh
```

Ref-1: https://www.pgadmin.org/download/pgadmin-4-apt/

Ref-2: https://www.youtube.com/watch?v=c_VFpEec5C4


### Database rename

- if your previous db is `my_database` and want to rename just type `alter database my_database rename to ph_db;`

```bash
postgres=# alter database my_database rename to ph_db;
```

### Database Drop

- if your db name is `test_db`

    ```bash
    postgres=# drop database test_db;
    ```


#### Alter - use for change

```sql
ALTER TABLE table_name action;
```


## 🔐 How to Reset PostgreSQL Password

### ✅ Step 1: Switch to `postgres` system user

```bash
sudo -i -u postgres
```

### ✅ Step 2: Access PostgreSQL shell

```bash
psql
```

### ✅ Step 3: Change the password

```bash
\password postgres
```
Then enter and confirm a new password.

### ✅ Step 4: Exit

```bash
\q
exit
```

### Now you can connect with prompt with the new password:

```bash
psql -U postgres -W
```