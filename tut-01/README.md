# Airflow tutorial

## Setup

```bash
# check python3 version
$ python3 --version

# install tooling for python3 environment on ubuntu
sudo  apt install python3.10-venv

# create a python environment
$ python3 -m venv py_env

# activate the python environment
$ source py_env/bin/activate

# install airflow locally from airflow github repository https://github.com/apache/airflow
# by copy/paste the install command from the github documentation
$ pip install 'apache-airflow==2.9.3' --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.9.3/constraints-3.10.txt"

# Setup airflow database by defining AIRFLOW_HOME
$ export AIRFLOW_HOME=`pwd`
$ airflow db init
$ airflow webserver -p 8080
$ airflow users create --help 
$ airflow users create --username admin --firstname firstname --lastname lastname --role Admin --email admin@domein.com
# asks for pwd: brtvpelt


# Start scheduler from separate session

# Setup airflow database by defining AIRFLOW_HOME
$ export AIRFLOW_HOME=`pwd`
# activate the python environment
$ source py_env/bin/activate

# start scheduler
$ airflow scheduler
```
  
