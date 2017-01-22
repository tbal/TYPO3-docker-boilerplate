[<-- Back to main section](../README.md)

# Running TYPO3

## Create TYPO3 project

For the first TYPO3 setup:

```bash
make create typo3
```

or (make sure [composer](https://getcomposer.org/) is installed)

```bash
rm -f app/.gitkeep
composer create-project typo3/cms-base-distribution app/
touch app/web/FIRST_INSTALL app/.gitkeep
```

Open <http://localhost:8000> and follow installation wizard.

When asked for database setup, use the settings from the [services documentation](https://github.com/webdevops/TYPO3-docker-boilerplate/blob/master/documentation/SERVICES.md#mysql) or see your `etc/environment.yml`. Make sure to set the correct database-host ('mysql' by default). 


Feel free to modify your TYPO3 installation in your `app/` (a shared folder of Docker),
most of the time there is no need to enter any Docker container.


## TYPO3 cli runner

You can run one-shot command inside the `app` service container:

```bash
docker-compose run --rm app web/typo3/cli_dispatch.phpsh extbase
# or simply:
docker-compose run --rm app cli extbase   # cli refers to CLI_SCRIPT env in etc/environment.yml

docker-compose run --rm app bash
```


## Error: Trusted Host pattern

Set in web/typo3conf/LocalConfiguration.php:

    'SYS' => array(
        [ ... ],
        'trustedHostsPattern' => '.*',
    ),

Should not be needed on Apache HTTPd.
