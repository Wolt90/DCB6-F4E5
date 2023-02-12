Скриншоты результатов запросов

![image](https://user-images.githubusercontent.com/125214665/218339254-5962d38d-1e58-441a-9cb6-4fed976bb7f3.png)
![image](https://user-images.githubusercontent.com/125214665/218339236-f53f18a5-9d7d-46cc-ba6a-3aeccce112ae.png)
![image](https://user-images.githubusercontent.com/125214665/218339261-35e572e3-0cdb-4d8f-a6d9-a45c9f52f20c.png)



# Development

1. Clone this repo & open with IDE (e.g. [VS Code](https://code.visualstudio.com/))

2. Prepare your development credentials for Clickhouse:

    - DBT_HOST
    - DBT_USER
    - DBT_PASSWORD

3. Install dbt environment with [Docker](https://docs.docker.com/desktop/#download-and-install):

    ```bash
    docker-compose up -d # build & run container

    docker-compose exec \
        dbt bash # execute dbt commands interactively
    ```

    <details><summary>Alternatively, install on local machine</summary>
    <p>

    [Install dbt](https://docs.getdbt.com/dbt-cli/install/overview) and [configure profile](https://docs.getdbt.com/dbt-cli/configure-your-profile) manually by yourself. By default, dbt expects the `profiles.yml` file to be located in the `~/.dbt/` directory.

    Use this template and enter your own credentials:

    ```yaml
    config:
        send_anonymous_usage_stats: False
        use_colors: True
        partial_parse: True

    clickhouse_starschema:
        target: dev
        outputs:
            dev:
                type: clickhouse
                schema: default
                host: "{{ env_var('DBT_HOST') }}"
                port: 8443
                user: "{{ env_var('DBT_USER') }}"
                password: "{{ env_var('DBT_PASSWORD') }}"
                secure: True
                verify: False
    ```
    </p>
    </details>
