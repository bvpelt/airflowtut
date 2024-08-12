# Airflow docker

Requirements
- docker installed [docker installation on ubuntu](https://docs.docker.com/engine/install/ubuntu/)
- docker compose installed [docker compose installation on linux](https://docs.docker.com/compose/install/linux/)


Check docker and docker compose

```bash
$ docker --version
Docker version 24.0.7, build 24.0.7-0ubuntu2~22.04.1

$ docker-compose --version
docker-compose version 1.29.2, build unknown

```

## Startup

Startup previous configuration from tut-02

```bash
$ echo -e "AIRFLOW_UID=$(id -u)" > .env

# restart
$ docker-compose up -d
```


## Remove default DAGs

```bash
# remove airflow containers and volumes
$ docker-compose down -v
Stopping tut-03_airflow-webserver_1 ... done
Stopping tut-03_airflow-scheduler_1 ... done
Stopping tut-03_airflow-triggerer_1 ... done
Stopping tut-03_postgres_1          ... done
Removing tut-03_airflow-webserver_1 ... done
Removing tut-03_airflow-scheduler_1 ... done
Removing tut-03_airflow-triggerer_1 ... done
Removing tut-03_airflow-init_1      ... done
Removing tut-03_postgres_1          ... done
Removing network tut-03_default
Removing volume tut-03_postgres-db-volume

# Reinitialize
$ docker-compose up airflow-init
Creating network "tut-03_default" with the default driver
Creating volume "tut-03_postgres-db-volume" with default driver
Creating tut-03_postgres_1 ... done
Creating tut-03_airflow-init_1 ... done
Attaching to tut-03_airflow-init_1
airflow-init_1       | The container is run as root user. For security, consider using a regular user account.
airflow-init_1       | 
airflow-init_1       | DB: postgresql+psycopg2://airflow:***@postgres/airflow
airflow-init_1       | Performing upgrade to the metadata database postgresql+psycopg2://airflow:***@postgres/airflow
airflow-init_1       | [2024-08-12T18:31:37.002+0000] {migration.py:215} INFO - Context impl PostgresqlImpl.
airflow-init_1       | [2024-08-12T18:31:37.002+0000] {migration.py:218} INFO - Will assume transactional DDL.
airflow-init_1       | [2024-08-12T18:31:37.003+0000] {migration.py:215} INFO - Context impl PostgresqlImpl.
airflow-init_1       | [2024-08-12T18:31:37.003+0000] {migration.py:218} INFO - Will assume transactional DDL.
airflow-init_1       | INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
airflow-init_1       | INFO  [alembic.runtime.migration] Will assume transactional DDL.
airflow-init_1       | INFO  [alembic.runtime.migration] Running stamp_revision  -> 686269002441
airflow-init_1       | Database migrating done!
airflow-init_1       | /home/airflow/.local/lib/python3.12/site-packages/flask_limiter/extension.py:333 UserWarning: Using the in-memory storage for tracking rate limits as no storage was explicitly specified. This is not recommended for production use. See: https://flask-limiter.readthedocs.io#configuring-a-storage-backend for documentation about configuring the storage backend.
airflow-init_1       | [2024-08-12T18:31:44.211+0000] {override.py:1454} INFO - Inserted Role: Admin
airflow-init_1       | [2024-08-12T18:31:44.220+0000] {override.py:1454} INFO - Inserted Role: Public
airflow-init_1       | [2024-08-12T18:31:44.222+0000] {override.py:951} WARNING - No user yet created, use flask fab command to do it.
airflow-init_1       | [2024-08-12T18:31:44.337+0000] {override.py:1858} INFO - Created Permission View: can edit on Passwords
airflow-init_1       | [2024-08-12T18:31:44.353+0000] {override.py:1909} INFO - Added Permission can edit on Passwords to role Admin
airflow-init_1       | [2024-08-12T18:31:44.378+0000] {override.py:1858} INFO - Created Permission View: can read on Passwords
airflow-init_1       | [2024-08-12T18:31:44.395+0000] {override.py:1909} INFO - Added Permission can read on Passwords to role Admin
airflow-init_1       | [2024-08-12T18:31:44.445+0000] {override.py:1858} INFO - Created Permission View: can edit on My Password
airflow-init_1       | [2024-08-12T18:31:44.462+0000] {override.py:1909} INFO - Added Permission can edit on My Password to role Admin
airflow-init_1       | [2024-08-12T18:31:44.487+0000] {override.py:1858} INFO - Created Permission View: can read on My Password
airflow-init_1       | [2024-08-12T18:31:44.503+0000] {override.py:1909} INFO - Added Permission can read on My Password to role Admin
airflow-init_1       | [2024-08-12T18:31:44.545+0000] {override.py:1858} INFO - Created Permission View: can edit on My Profile
airflow-init_1       | [2024-08-12T18:31:44.562+0000] {override.py:1909} INFO - Added Permission can edit on My Profile to role Admin
airflow-init_1       | [2024-08-12T18:31:44.587+0000] {override.py:1858} INFO - Created Permission View: can read on My Profile
airflow-init_1       | [2024-08-12T18:31:44.603+0000] {override.py:1909} INFO - Added Permission can read on My Profile to role Admin
airflow-init_1       | [2024-08-12T18:31:44.687+0000] {override.py:1858} INFO - Created Permission View: can create on Users
airflow-init_1       | [2024-08-12T18:31:44.703+0000] {override.py:1909} INFO - Added Permission can create on Users to role Admin
airflow-init_1       | [2024-08-12T18:31:44.770+0000] {override.py:1858} INFO - Created Permission View: can read on Users
airflow-init_1       | [2024-08-12T18:31:44.787+0000] {override.py:1909} INFO - Added Permission can read on Users to role Admin
airflow-init_1       | [2024-08-12T18:31:44.812+0000] {override.py:1858} INFO - Created Permission View: can edit on Users
airflow-init_1       | [2024-08-12T18:31:44.828+0000] {override.py:1909} INFO - Added Permission can edit on Users to role Admin
airflow-init_1       | [2024-08-12T18:31:44.853+0000] {override.py:1858} INFO - Created Permission View: can delete on Users
airflow-init_1       | [2024-08-12T18:31:44.870+0000] {override.py:1909} INFO - Added Permission can delete on Users to role Admin
airflow-init_1       | [2024-08-12T18:31:44.912+0000] {override.py:1858} INFO - Created Permission View: menu access on List Users
airflow-init_1       | [2024-08-12T18:31:44.928+0000] {override.py:1909} INFO - Added Permission menu access on List Users to role Admin
airflow-init_1       | [2024-08-12T18:31:44.962+0000] {override.py:1858} INFO - Created Permission View: menu access on Security
airflow-init_1       | [2024-08-12T18:31:45.058+0000] {override.py:1909} INFO - Added Permission menu access on Security to role Admin
airflow-init_1       | [2024-08-12T18:31:45.128+0000] {override.py:1858} INFO - Created Permission View: can create on Roles
airflow-init_1       | [2024-08-12T18:31:45.136+0000] {override.py:1909} INFO - Added Permission can create on Roles to role Admin
airflow-init_1       | [2024-08-12T18:31:45.145+0000] {override.py:1858} INFO - Created Permission View: can read on Roles
airflow-init_1       | [2024-08-12T18:31:45.153+0000] {override.py:1909} INFO - Added Permission can read on Roles to role Admin
airflow-init_1       | [2024-08-12T18:31:45.161+0000] {override.py:1858} INFO - Created Permission View: can edit on Roles
airflow-init_1       | [2024-08-12T18:31:45.170+0000] {override.py:1909} INFO - Added Permission can edit on Roles to role Admin
airflow-init_1       | [2024-08-12T18:31:45.178+0000] {override.py:1858} INFO - Created Permission View: can delete on Roles
airflow-init_1       | [2024-08-12T18:31:45.186+0000] {override.py:1909} INFO - Added Permission can delete on Roles to role Admin
airflow-init_1       | [2024-08-12T18:31:45.203+0000] {override.py:1858} INFO - Created Permission View: menu access on List Roles
airflow-init_1       | [2024-08-12T18:31:45.211+0000] {override.py:1909} INFO - Added Permission menu access on List Roles to role Admin
airflow-init_1       | [2024-08-12T18:31:45.403+0000] {override.py:1858} INFO - Created Permission View: can read on User Stats Chart
airflow-init_1       | [2024-08-12T18:31:45.420+0000] {override.py:1909} INFO - Added Permission can read on User Stats Chart to role Admin
airflow-init_1       | [2024-08-12T18:31:45.453+0000] {override.py:1858} INFO - Created Permission View: menu access on User's Statistics
airflow-init_1       | [2024-08-12T18:31:45.470+0000] {override.py:1909} INFO - Added Permission menu access on User's Statistics to role Admin
airflow-init_1       | [2024-08-12T18:31:45.537+0000] {override.py:1858} INFO - Created Permission View: can read on Permissions
airflow-init_1       | [2024-08-12T18:31:45.553+0000] {override.py:1909} INFO - Added Permission can read on Permissions to role Admin
airflow-init_1       | [2024-08-12T18:31:45.586+0000] {override.py:1858} INFO - Created Permission View: menu access on Actions
airflow-init_1       | [2024-08-12T18:31:45.603+0000] {override.py:1909} INFO - Added Permission menu access on Actions to role Admin
airflow-init_1       | [2024-08-12T18:31:45.645+0000] {override.py:1858} INFO - Created Permission View: can read on View Menus
airflow-init_1       | [2024-08-12T18:31:45.653+0000] {override.py:1909} INFO - Added Permission can read on View Menus to role Admin
airflow-init_1       | [2024-08-12T18:31:45.670+0000] {override.py:1858} INFO - Created Permission View: menu access on Resources
airflow-init_1       | [2024-08-12T18:31:45.678+0000] {override.py:1909} INFO - Added Permission menu access on Resources to role Admin
airflow-init_1       | [2024-08-12T18:31:45.711+0000] {override.py:1858} INFO - Created Permission View: can read on Permission Views
airflow-init_1       | [2024-08-12T18:31:45.720+0000] {override.py:1909} INFO - Added Permission can read on Permission Views to role Admin
airflow-init_1       | [2024-08-12T18:31:45.737+0000] {override.py:1858} INFO - Created Permission View: menu access on Permission Pairs
airflow-init_1       | [2024-08-12T18:31:45.753+0000] {override.py:1909} INFO - Added Permission menu access on Permission Pairs to role Admin
airflow-init_1       | [2024-08-12T18:31:46.512+0000] {override.py:1543} INFO - Added user airflow
airflow-init_1       | User "airflow" created with role "Admin"
airflow-init_1       | 2.9.3
tut-03_airflow-init_1 exited with code 0

# start airflow again
$ docker-compose up -d
tut-03_postgres_1 is up-to-date
Starting tut-03_airflow-init_1 ... done
Creating tut-03_airflow-scheduler_1 ... done
Creating tut-03_airflow-triggerer_1 ... done
Creating tut-03_airflow-webserver_1 ... done
```

Wait 2 minutes and open airflow webapp at http://0.0.0.0:8080 and loging with default credentials airflow:airflow


