# mock-wp-docker

## Installation

Replace domain in db data to local domain

```bash
ag -lr ${domain} | xargs sed -n -e 's/${domain}/http:\/\/local\.mock-wp\.com/gp'
ag -lr ${domain} | xargs sed -i "" -e 's/${domain}/http:\/\/local\.mock-wp\.com/g'
```

Copy initial DB data at `containers/db/init/local`

```bash
cp ${init data} ./containers/db/init/local
```

Set .env for MySQL Container

```
APACHE_LOG_DIR=/var/log/apache2

MYSQL_DATABASE=
MYSQL_USER=
MYSQL_PASSWORD=
MYSQL_ROOT_PASSWORD=
```

Build wp containers

```bash
COMPOSE_FILE=docker-compose.local.yml docker-compose up --build
```

Modify DB access info at `wp-config.php`

```bash
/** MySQL hostname */
-define('DB_HOST', '${your db host}');
+define('DB_HOST', 'db');

-define('WP_DEBUG', false);
+define('WP_DEBUG', true);
```
