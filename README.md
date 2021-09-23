# TEST DE PROGRAMADOR

## Pregunta 1
Necesita crear una tabla llamada ‘countries’ que tendrá una lista de países. En Laravel, indique que comando (o comandos) de Artisan se requiere para crear los ficheros del “model”, “database migration” y “seeder” y a su vez, indique que nombres y ubicaciones tendrán los archivos generados, según el estándar Laravel. Considere que el comando se ejecuta el día 23/09/2021 a las 00:00:00 y que está utilizando una versión de Laravel 7 o superior.

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
Está trabajando el backend de un blog en Lumen, y requiere generar una ruta para un comentario, esta ruta debe tener el formato **posts/5/comments/25** donde 5 es el ID del post y 25 es el ID del comentario. Indique como debe generar esa ruta publica básica, para efectos de la prueba, considere que debe devolver un simple array que contiene el *post_id* y el *comment_id*

### Repuesta
``` php
$router->get('posts/{postId}/comments/{commentId}', function ($post_id, $comment_id) {
    return [
        'post_id' => $post_id,
        'comment_id' => $comment_id
    ]
});
```

## Pregunta 3
Está desarrollando un sistema para una concesionaria de automóviles, tiene una base de datos en MySQL con las tablas brands y models. Una marca de autos (brand) tiene uno o mas modelos asociados (models). Los campos de las tablas son las siguientes:
* Tabla brand: id, name
* Tabla model: id, brand_id, name
<p>Genere una consulta que arroje los modelos correspondientes a la marca que tiene como *name* exactamente **Audi**. Para identificar mejor, los campos del resultado deben ser model_id (campo id del model) y model (campos name del model)

### Respuesta
``` sql
SELECT m.id as model_id, m.name as model
FROM brands as b
JOIN models as m ON m.brand_id = b.id
WHERE b.name = "Audi"
```

## Pregunta 4
Está trabajando con una base de datos MongoDB que tiene una colección llamada *users* con los atributos "nombre" y "rol" . Indique que comando a realizar para insertar los datos del usuario "Juan Perez" que será un "Admin"

### Respuesta
``` json
db.users.insert( {
                     nombre: "Juan Perez",
                     rol: "Admin"
            }
  )
```

## Pregunta 5
Está desarrollando la pantalla de login de un usuario en Vue.js. En la parte del Javascript tiene la variable **name** con el nombre del usuario y la función **notificaciones** que devuelve *true* o *false* en caso tenga o no tenga notificaciones. 
Indique como debe poner en el template para que se muestre el mensaje:
**Hola Juan, tiene nuevas notificaciones**
Solo en el caso que Juan tenga nuevas notificaciones.

### Respuesta
``` html
<p v-if="seen">Agora você me viu</p>
```

## Pregunta 6
Tiene la tabla **years** en una base de datos SQL Server, que corresponde a los años y tiene los campos **id** y **year** (que corresponde al número del año). Se requiere filtrar los registros que corresponden a los años pares entre 1995 y 2015, ordenados de mayor a menor según el año. Indique que consulta SQL devuelve los datos requeridos

### Respuesta
``` sql
SELECT * FROM `years`
WHERE year BETWEEN 1995 AND 2015 
AND year % 2 = 0;
GO
```

select num from table where ( num % 2 ) = 0

## Pregunta 7
En Laravel, indique como debe ser la definición de los campos que debe tener el fichero del *“database migration”* de la tabla **currencies** que tendrá los campos **code** (código internacional único de la moneda representado por 3 caracteres, Ej ‘PEN’), **name** (nombre de la moneda, Ej: ‘Nuevos Soles’) y **symbol** (símbolo de la moneda, Ej: ‘S/.’). Esta tabla no tendrá un ID numérico autoincremental, pues el campo code debe ser el **primario**.

### Respuesta
``` php
    Schema::create('currencies', function (Blueprint $table) {
        $table->string('code',3);
        $table->string('name');
        $table->string('symbol');
        $table->primary(['code']);
    });
```

## Pregunta 8
Con la misma tabla del ejercicio anterior **currencies**, indique que debe agregar en el fichero del modelo Currency dentro de la definición de la clase Currency, para considerar que la tabla **no tendrá** valor ID incremental, que el **primario** será el campo **code** que es un **string** y no un entero, y que la tabla **no tendrá** timestamps de creación y modificación.

``` php
    class Currency extends Model
    {
        // Esta es la definición requerida
        public $incrementing = false;
        protected $keyType = 'string';
        protected $primaryKey = 'code';
        public $timestamps = false;

    }
```

## Pregunta 9
Está desarrollando el frontend en Vue.js de un sistema e-learning y debe mostrar la lista de cursos en donde el usuario está matriculado. En el javascript tiene la variable **_cursos_** que es un array que contiene la lista de cursos (campos **nombreCurso** y **fechaMatricula**). Indique como se puede mostrar en un listado `<ul>` la lista de cursos, por ejemplo con la fecha de matrícula entre paréntesis, Ej: **Introducción a Vue (23/09/2021)**. En caso no esté matriculado en ningún curso, deberá mostrar el mensaje **No está matriculado en ningún curso**
La respuesta puede estar en template o en una función render.

### Respuesta
```javascript
//Respuesta válida template:
<ul v-if="cursos.length">
  <li v-for="item in cursos">{{ item.nombreCurso }} ( {{ item.fechaMatricula }})</li>
</ul>
<p v-else>No está matriculado en ningún curso</p>

//Respuesta válida render:
props: ['cursos'],
render: function (createElement) {
  if (this.cursos.length) {
    return createElement('ul', this.items.map(function (item) {
      return createElement('li', `${ item.nombreCurso } (${ item.fechaMatricula })`)
    }))
  } else {
    return createElement('p', 'No está matriculado en ningún curso')
  }
}
```

## Pregunta 10
Tiene una tabla en una base de datos MySQL con el nombre de **products** que tiene los campos **id** (int), **name** (varchar), y **stock** (int). Indique el Query que devuelve la relación de los productos con su stock, pero que cuando el stock sea 0, el campo del stock debe devolver la frase “Sin stock”.

### Respuesta
```sql
SELECT id, name, (CASE WHEN stock > 0 THEN CAST(stock as CHAR(50)) ELSE 'Sin stock' END) as stock
FROM products
```

## Pregunta 11
Tiene una colección de usuarios en MongoDB que tiene los atributos: **nombre**, **pais**. Se requiere la lista de los usuarios cuyo país es Perú, ordenados alfabéticamente por el nombre en forma descendente. Indicar que comando devuelve lo solicitado.

### Respuesta
``` javascript
db.usuarios.find({pais : "Perú"}).sort({noombre:-1})
```

## Pregunta 12
Indique el resultado de la siguiente expresión en SQL:
### **SELECT COALESCE(NULL,  NULL, ‘Juan’, NULL, ‘Pedro’, NULL, NULL, ‘Maria’);**

### Respueta
``` sql
Juan
```

## Pregunta 13
En Laravel, tiene ya definida la ruta tipo POST **“/multiplica”** que ejecuta una función que se encuentra en cierto controlador. La respuesta debe devolver la multiplicación de 2 números que fueron pasados en un JSON que tiene la forma
``` json
{
	number1: 20,
	number2: 4
}
```
Defina la función que retorna el siguiente JSON de ejemplo:
``` json
{
	result: 80
}
```

### Respuesta
``` php
public function Multiplica (Request $request)
{
    return [
        'result' => $request->input('number1') * $request->input('number2');
    ]
}
```

## Pregunta 14
En Lumen, está trabajando una función que recibe como parámetros las variables **$content** (que ya tiene el contenido de lo que debe devolver) y **$mime** (que es el **tipo de MIME** del **$content**, por ejemplo: *application/pdf* ). Escriba su función que devuelve el $content con el **header ‘Content-Type’** que tiene el valor del $mime. Puede definir su función con el nombre que mejor crea conveniente.

### Respuesta
``` php
function Respuesta($content, $mime)
{
    return response($content)
                ->withHeaders([
                    'Content-Type' => $mime
                ]);
}
```

## Pregunta 15
En Laravel, tiene los modelos **Category** y **Product**, donde un Category puede tener muchos Products. Complete la definición de sus modelos Category y Product:
``` php
Class Category extends Model
{
// Aqui debe completer su respuesta
}
``` 
``` php
Class Product extends Model
{
// Aqui debe completer su respuesta
}
``` 
Para que sea posible realizar lo siguiente en algún controlador:
```php 
use App\Models\Category
use App\Models\Product
….
	// $products contiene la lista de productos de la categoría con id 1:
    $products = Category::find(1)->products;
	// $category contiene la categoria del producto con id 1:
	$category = Product::find(1)->category
```

### Respuesta
``` php
Class Category extends Model
{
    public function products()
    {
        return $this->hasMany(Product::class);
    }
}
``` 
``` php
Class Product extends Model
{
    public function category()
    {
        return $this->belongsTo(Category::class);
    }   
}
```