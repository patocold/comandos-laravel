<p align="center"><img src="https://res.cloudinary.com/dtfbvvkyp/image/upload/v1566331377/laravel-logolockup-cmyk-red.svg" width="400"></p>


# Comandos Laravel
## Crear un modelo desde 0

_Una serie de ejemplos paso a paso que te dice lo que debes ejecutar para tener un entorno de desarrollo ejecutandose_

```
php artisan make:model Modelo -m
```

_`-m` para crear la migración_
_`-f` para crear la factoria_
```
    /*
	|--------------------------------------------------------------------------
	| GLOBAL VARIABLES
	|--------------------------------------------------------------------------
    */

    //protected $table = 'nombreDeLaTabla';
    //protected $primaryKey = 'id';
    //public $timestamps = false;
    //protected $guarded = ['id'];
    protected $fillable = [
        'columna1',
        'columna2',
        'columna3',
    ];
    // protected $hidden = [];
    // protected $dates = [];

    /*
	|--------------------------------------------------------------------------
	| EVENTS
	|--------------------------------------------------------------------------
    */
    /*
	|--------------------------------------------------------------------------
	| FUNCTIONS
	|--------------------------------------------------------------------------
    */
    /*
	|--------------------------------------------------------------------------
	| RELATIONS
	|--------------------------------------------------------------------------
    */
    /*
    |--------------------------------------------------------------------------
    | SCOPES
    |--------------------------------------------------------------------------
    */
    /*
	|--------------------------------------------------------------------------
	| ACCESORS
	|--------------------------------------------------------------------------
    */
    /*
	|--------------------------------------------------------------------------
	| MUTATORS
	|--------------------------------------------------------------------------
	*/
```
_foreignKey_
```php
$table->unsignedBigInteger('user_id');
$table->foreign('user_id')
    ->references('id')
    ->on('users')
    ->onUpdate('no action')
    ->onDelete('no action');
```