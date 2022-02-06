# Docker Bedrock Local

This bootstraps a local docker development environment for Wordpress
sites using [Bedrock](https://roots.io/bedrock/).

```shell
# Create Bedrock project as per https://roots.io/bedrock/
composer create-project roots/bedrock myproject

# CD into the project directory
cd myproject

# Install this library
composer require wpwildfire/docker-bedrock-local --dev

# Symlink the docker-compose.yml file to the root of the project
ln -f ./vendor/wpwildfire/docker-bedrock-local/docker-compose.yml ./docker-compose.yml

# Add your desired PHP version to the bedrock-generated .env file
echo "PHP_VERSION=7.4" >> .env

# Update the WP_HOME var to http://localhost:8080 in the Bedrock generated .env file
sed -i "s/WP_HOME=[^\"]*/WP_HOME=\"http:\/\/localhost:8080\"/g;" .env

# Run docker compose up to run the environment
docker-compose up --build
```

Once the environment comes up, you will be able to access Wordpress
at http://localhost:8080

If you wish to install a specific PHP version, you can pass it in using
the `PHP_VERSION` environment variable (instead of a adding
a version number to the `.env` file):
```shell
export PHP_VERSION=8.1; docker-compose up --build
```

This docker-compose fires up the following containers with 
appropriate development-related settings and configuration.

* [Nginx Official](https://hub.docker.com/_/nginx/) - Unmodified
* [Wordpress Official](https://hub.docker.com/_/wordpress/) - Modified to add Wordpress CLI, Composer, XDebug and PHPUnit
* [MySQL Official](https://hub.docker.com/_/mysql) - Unmodified
* [Mailhog Official](https://hub.docker.com/r/mailhog/mailhog) - Unmodified

Please note: This docker environment is absolutely NOT production
ready, and should never be used in any public-facing environments.

## Mail
All mail sent from this environment will be captured in Mailhog
and can be viewed in the Mailhog interface on http://localhost:8025/
 