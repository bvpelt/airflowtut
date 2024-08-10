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

## Setup

Get airflow docker compose file [download link](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html)

```bash
$ curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.9.3/docker-compose.yaml'
```

Make changes to the docker-compose.yaml file [adapted docker-compose.yaml](docker-compose.yaml)

Create directories
- ./dags - you can put your DAG files here.
- ./logs - contains logs from task execution and scheduler.
- ./config - you can add custom log parser or add airflow_local_settings.py to configure cluster policy.
- ./plugins - you can put your custom plugins here.

On Linux, the quick-start needs to know your host user id and needs to have group id set to 0. Otherwise the files created in dags, logs and plugins will be created with root user ownership. You have to make sure to configure them for the docker-compose:

```bash
$ mkdir -p ./dags ./logs ./plugins ./config
$ echo -e "AIRFLOW_UID=$(id -u)" > .env
```

Initialize the database

```bash
$ docker-compose up airflow-init
Creating network "tut-02_default" with the default driver
Creating volume "tut-02_postgres-db-volume" with default driver
Pulling postgres (postgres:13)...
13: Pulling from library/postgres
efc2b5ad9eec: Pull complete
01140ce64c0f: Pull complete
6467a2fcd858: Pull complete
349338617ae2: Pull complete
3b5eb083a655: Pull complete
ac1f4d123350: Pull complete
dcd8f923e5cf: Pull complete
bafad3d3bd30: Pull complete
3a4daa5ddab5: Pull complete
55b3e5f140b9: Pull complete
4b38237cd96c: Pull complete
8c6d5aba0cdb: Pull complete
d76790c469eb: Pull complete
0769e4313d71: Pull complete
Digest: sha256:aca851750cd95182cdfd0b4856e31425ca6b921e44703c789d76b463be0b4e88
Status: Downloaded newer image for postgres:13
Pulling airflow-init (apache/airflow:2.9.3)...
2.9.3: Pulling from apache/airflow
efc2b5ad9eec: Already exists
62eefda23922: Pull complete
31a912153c27: Pull complete
9597e1b644c5: Pull complete
a2dc9bc0cbbd: Pull complete
1b4ce37578e3: Pull complete
fd5a2489b8e6: Pull complete
3fde7a0ef3b3: Pull complete
91e26d8fd5e2: Pull complete
973091cd6b99: Pull complete
bae04197dad2: Pull complete
4563681f31bc: Pull complete
f983fce4639d: Pull complete
804e344abf30: Pull complete
2704d283b94f: Pull complete
59d0aded76d4: Pull complete
9eab37d5ecb1: Pull complete
0e13362e6bc9: Pull complete
af9be525ecb7: Pull complete
dc2e6ca0f816: Pull complete
7bdef287746a: Pull complete
4f4fb700ef54: Pull complete
Digest: sha256:0188b06abb250caccc48bb6d00fde5e74a211273f78b0d143bc4d63f2b67412d
Status: Downloaded newer image for apache/airflow:2.9.3
Creating tut-02_postgres_1 ... done
Creating tut-02_airflow-init_1 ... done
Attaching to tut-02_airflow-init_1
airflow-init_1       | The container is run as root user. For security, consider using a regular user account.
airflow-init_1       | 
airflow-init_1       | DB: postgresql+psycopg2://airflow:***@postgres/airflow
airflow-init_1       | Performing upgrade to the metadata database postgresql+psycopg2://airflow:***@postgres/airflow
airflow-init_1       | [2024-08-10T18:13:19.616+0000] {migration.py:215} INFO - Context impl PostgresqlImpl.
airflow-init_1       | [2024-08-10T18:13:19.616+0000] {migration.py:218} INFO - Will assume transactional DDL.
airflow-init_1       | [2024-08-10T18:13:19.617+0000] {migration.py:215} INFO - Context impl PostgresqlImpl.
airflow-init_1       | [2024-08-10T18:13:19.617+0000] {migration.py:218} INFO - Will assume transactional DDL.
airflow-init_1       | INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
airflow-init_1       | INFO  [alembic.runtime.migration] Will assume transactional DDL.
airflow-init_1       | INFO  [alembic.runtime.migration] Running stamp_revision  -> 686269002441
airflow-init_1       | Database migrating done!
airflow-init_1       | /home/airflow/.local/lib/python3.12/site-packages/flask_limiter/extension.py:333 UserWarning: Using the in-memory storage for tracking rate limits as no storage was explicitly specified. This is not recommended for production use. See: https://flask-limiter.readthedocs.io#configuring-a-storage-backend for documentation about configuring the storage backend.
airflow-init_1       | [2024-08-10T18:13:26.392+0000] {override.py:1454} INFO - Inserted Role: Admin
airflow-init_1       | [2024-08-10T18:13:26.400+0000] {override.py:1454} INFO - Inserted Role: Public
airflow-init_1       | [2024-08-10T18:13:26.403+0000] {override.py:951} WARNING - No user yet created, use flask fab command to do it.
airflow-init_1       | [2024-08-10T18:13:26.534+0000] {override.py:1858} INFO - Created Permission View: can edit on Passwords
airflow-init_1       | [2024-08-10T18:13:26.551+0000] {override.py:1909} INFO - Added Permission can edit on Passwords to role Admin
airflow-init_1       | [2024-08-10T18:13:26.575+0000] {override.py:1858} INFO - Created Permission View: can read on Passwords
airflow-init_1       | [2024-08-10T18:13:26.584+0000] {override.py:1909} INFO - Added Permission can read on Passwords to role Admin
airflow-init_1       | [2024-08-10T18:13:26.609+0000] {override.py:1858} INFO - Created Permission View: can edit on My Password
airflow-init_1       | [2024-08-10T18:13:26.617+0000] {override.py:1909} INFO - Added Permission can edit on My Password to role Admin
airflow-init_1       | [2024-08-10T18:13:26.625+0000] {override.py:1858} INFO - Created Permission View: can read on My Password
airflow-init_1       | [2024-08-10T18:13:26.634+0000] {override.py:1909} INFO - Added Permission can read on My Password to role Admin
airflow-init_1       | [2024-08-10T18:13:26.659+0000] {override.py:1858} INFO - Created Permission View: can edit on My Profile
airflow-init_1       | [2024-08-10T18:13:26.667+0000] {override.py:1909} INFO - Added Permission can edit on My Profile to role Admin
airflow-init_1       | [2024-08-10T18:13:26.684+0000] {override.py:1858} INFO - Created Permission View: can read on My Profile
airflow-init_1       | [2024-08-10T18:13:26.701+0000] {override.py:1909} INFO - Added Permission can read on My Profile to role Admin
airflow-init_1       | [2024-08-10T18:13:26.842+0000] {override.py:1858} INFO - Created Permission View: can create on Users
airflow-init_1       | [2024-08-10T18:13:26.851+0000] {override.py:1909} INFO - Added Permission can create on Users to role Admin
airflow-init_1       | [2024-08-10T18:13:26.876+0000] {override.py:1858} INFO - Created Permission View: can read on Users
airflow-init_1       | [2024-08-10T18:13:26.892+0000] {override.py:1909} INFO - Added Permission can read on Users to role Admin
airflow-init_1       | [2024-08-10T18:13:26.917+0000] {override.py:1858} INFO - Created Permission View: can edit on Users
airflow-init_1       | [2024-08-10T18:13:26.934+0000] {override.py:1909} INFO - Added Permission can edit on Users to role Admin
airflow-init_1       | [2024-08-10T18:13:26.959+0000] {override.py:1858} INFO - Created Permission View: can delete on Users
airflow-init_1       | [2024-08-10T18:13:26.976+0000] {override.py:1909} INFO - Added Permission can delete on Users to role Admin
airflow-init_1       | [2024-08-10T18:13:27.017+0000] {override.py:1858} INFO - Created Permission View: menu access on List Users
airflow-init_1       | [2024-08-10T18:13:27.025+0000] {override.py:1909} INFO - Added Permission menu access on List Users to role Admin
airflow-init_1       | [2024-08-10T18:13:27.051+0000] {override.py:1858} INFO - Created Permission View: menu access on Security
airflow-init_1       | [2024-08-10T18:13:27.059+0000] {override.py:1909} INFO - Added Permission menu access on Security to role Admin
airflow-init_1       | [2024-08-10T18:13:27.109+0000] {override.py:1858} INFO - Created Permission View: can create on Roles
airflow-init_1       | [2024-08-10T18:13:27.117+0000] {override.py:1909} INFO - Added Permission can create on Roles to role Admin
airflow-init_1       | [2024-08-10T18:13:27.125+0000] {override.py:1858} INFO - Created Permission View: can read on Roles
airflow-init_1       | [2024-08-10T18:13:27.134+0000] {override.py:1909} INFO - Added Permission can read on Roles to role Admin
airflow-init_1       | [2024-08-10T18:13:27.142+0000] {override.py:1858} INFO - Created Permission View: can edit on Roles
airflow-init_1       | [2024-08-10T18:13:27.150+0000] {override.py:1909} INFO - Added Permission can edit on Roles to role Admin
airflow-init_1       | [2024-08-10T18:13:27.159+0000] {override.py:1858} INFO - Created Permission View: can delete on Roles
airflow-init_1       | [2024-08-10T18:13:27.167+0000] {override.py:1909} INFO - Added Permission can delete on Roles to role Admin
airflow-init_1       | [2024-08-10T18:13:27.184+0000] {override.py:1858} INFO - Created Permission View: menu access on List Roles
airflow-init_1       | [2024-08-10T18:13:27.192+0000] {override.py:1909} INFO - Added Permission menu access on List Roles to role Admin
airflow-init_1       | [2024-08-10T18:13:27.225+0000] {override.py:1858} INFO - Created Permission View: can read on User Stats Chart
airflow-init_1       | [2024-08-10T18:13:27.234+0000] {override.py:1909} INFO - Added Permission can read on User Stats Chart to role Admin
airflow-init_1       | [2024-08-10T18:13:27.259+0000] {override.py:1858} INFO - Created Permission View: menu access on User's Statistics
airflow-init_1       | [2024-08-10T18:13:27.267+0000] {override.py:1909} INFO - Added Permission menu access on User's Statistics to role Admin
airflow-init_1       | [2024-08-10T18:13:27.325+0000] {override.py:1858} INFO - Created Permission View: can read on Permissions
airflow-init_1       | [2024-08-10T18:13:27.334+0000] {override.py:1909} INFO - Added Permission can read on Permissions to role Admin
airflow-init_1       | [2024-08-10T18:13:27.350+0000] {override.py:1858} INFO - Created Permission View: menu access on Actions
airflow-init_1       | [2024-08-10T18:13:27.359+0000] {override.py:1909} INFO - Added Permission menu access on Actions to role Admin
airflow-init_1       | [2024-08-10T18:13:27.392+0000] {override.py:1858} INFO - Created Permission View: can read on View Menus
airflow-init_1       | [2024-08-10T18:13:27.400+0000] {override.py:1909} INFO - Added Permission can read on View Menus to role Admin
airflow-init_1       | [2024-08-10T18:13:27.425+0000] {override.py:1858} INFO - Created Permission View: menu access on Resources
airflow-init_1       | [2024-08-10T18:13:27.442+0000] {override.py:1909} INFO - Added Permission menu access on Resources to role Admin
airflow-init_1       | [2024-08-10T18:13:27.551+0000] {override.py:1858} INFO - Created Permission View: can read on Permission Views
airflow-init_1       | [2024-08-10T18:13:27.567+0000] {override.py:1909} INFO - Added Permission can read on Permission Views to role Admin
airflow-init_1       | [2024-08-10T18:13:27.601+0000] {override.py:1858} INFO - Created Permission View: menu access on Permission Pairs
airflow-init_1       | [2024-08-10T18:13:27.617+0000] {override.py:1909} INFO - Added Permission menu access on Permission Pairs to role Admin
airflow-init_1       | [2024-08-10T18:13:28.325+0000] {override.py:1543} INFO - Added user airflow
airflow-init_1       | User "airflow" created with role "Admin"
airflow-init_1       | 2.9.3
tut-02_airflow-init_1 exited with code 0
```

Startup airflow by running docker-compose in detached mode

```bash
$ docker-compose up -d
tut-02_postgres_1 is up-to-date
Starting tut-02_airflow-init_1 ... done
Creating tut-02_airflow-scheduler_1 ... done
Creating tut-02_airflow-triggerer_1 ... done
Creating tut-02_airflow-webserver_1 ... done

# check started docker containers
$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS                    PORTS                    NAMES
5bcbae7a4391   apache/airflow:2.9.3   "/usr/bin/dumb-init …"   36 seconds ago   Up 32 seconds (healthy)   0.0.0.0:8080->8080/tcp   tut-02_airflow-webserver_1
1a0cf6313eca   apache/airflow:2.9.3   "/usr/bin/dumb-init …"   36 seconds ago   Up 32 seconds (healthy)   8080/tcp                 tut-02_airflow-triggerer_1
a92d73788649   apache/airflow:2.9.3   "/usr/bin/dumb-init …"   36 seconds ago   Up 33 seconds (healthy)   8080/tcp                 tut-02_airflow-scheduler_1
a6ef16940443   postgres:13            "docker-entrypoint.s…"   4 minutes ago    Up 4 minutes (healthy)    5432/tcp                 tut-02_postgres_1
```

Open airflow webapp at http://0.0.0.0:8080 and loging with default credentials admin:admin

Select DAG example_bash_operator and start it
[opened webserver after running DAG example_bash_operator](./webserver.png)

