# Airflow-celery-template

Fully dockerized template for airflow setup with celery executor with rabbitmq as broker.

Each component of airflow has a separate container

**Components**

- `airflow-webserver` to server airflow gui
- `airflow-scheduler` to server airflow gui
- `airflow-worker-i` celery worker i
- `flower` flower dashboard
- `postgres` result backend for broker
- `rabbitmq` celery broker
- `nginx` proxy to map all the dashboards at 1 place

And a container to initialize the airflow db -> `airflow-init`

## Running

- Create a .env by using env.example as reference
  ```
    $ cp env.example .env
  ```
  And not change the values in .env

- Run the init container to initialize database
  ```
    $ docker-compose up airflow-init
  ```
  This will initialize the database for airflow and create a default user using the details in
  .env (`AIRFLOW_ADMIN_USER` and `AIRFLOW_ADMIN_PASS`). At the end you should see a message like
  `Admin user created`

- Run the whole stack
  ```
    $ docker-compose up -d
  ```

The whole stack should be up and running at [http://localhost:80](http://localhost:80)

- Rabbitmq at `/`
- Airflow dashboard at `/airflow/`
- Flower dashboard at `/flower/`

## Acknowledgements

This is a modified version of the official docker-compose template of airflow
given [here](https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html#:~:text=To%20deploy%20Airflow%20on%20Docker,yaml.&text=This%20file%20contains%20several%20service,once%20their%20dependencies%20are%20complete.)
