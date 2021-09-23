# TEST DE PROGRAMSDOR

## Pregunta 1
En mi base de datos, necesito crear una tabla llamada ‘countries’ que tendrá una lista de países. En Laravel, indique que comando (o comandos) de Artisan se requiere para crear los ficheros del “model”, “database migration” y “seeder” y a su vez, indique que nombres y ubicaciones tendrán los archivos generados, según el estándar Laravel. Considere que el comando se ejecuta el día 23/09/2021 a las 00:00:00 y que está utilizando una versión de Laravel 7 o superior.

### Respuesta
*Comandos para generacion de archivos*
``` bash
# Respuesta váida 1:
$ php artisan make:model Country --migration --seed

# Respuesta váida 2:
$ php artisan make:model Country --m –s

# Respuesta váida 3:
$ php artisan make:model Country –migration
$ php artisan make:seeder CountrySeeder

# Respuesta válida 4:
php artisan make:model Country
php artisan make:migration create_countries_table
php artisan make:seeder CountrySeeder
```
*Rutas y ficheros creados*
* app/Models/Country.php
* database/migrations/2021_09_23_000000_create_countries_table.php
* database/seeders/CountrySeeder.php

## Pregunta 2