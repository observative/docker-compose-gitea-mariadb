# Docker gitea mariadb 
## [Gitea](https://gitea.io/) is a painless self-hosted Git service

### Getting started

1. Clone project :

    ```sh
    git clone https://github.com/observative/docker-gitea-mariadb
    ```

2. You could customize your settings before installation :

    Edit `.env` file

3. Install :

    ```sh
    # Copy the configuration file from the dist file
    cp etc/app.ini.dist etc/app.ini

    # Start services
    sudo docker-compose up -d

    # Generate self-signed certificates
    source .env && sudo docker-compose exec -T gitea-app bash -c "cd /app/gitea; exec /app/gitea/gitea cert -ca=true -duration=$GITEA_CERT_DURATION -host=$GITEA_VIRTUAL_HOST"

    # Copy the configuration file to the container
    sudo docker cp $(pwd)/etc/app.ini $(sudo docker-compose ps -q gitea-app):/data/gitea/conf/app.ini

    sudo docker cp $(pwd)/etc/templates $(sudo docker-compose ps -q gitea-app):/data/gitea/

    # Restart the server to reload the configuration
    sudo docker-compose restart gitea-app

    ```
