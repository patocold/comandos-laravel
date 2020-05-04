<p align="center"><img src="https://res.cloudinary.com/dtfbvvkyp/image/upload/v1566331377/laravel-logolockup-cmyk-red.svg" width="400"></p>


# Comandos Laravel
## Crear un modelo desde 0

_Una serie de ejemplos paso a paso que te dice lo que debes ejecutar para tener un entorno de desarrollo ejecutandose_

```
php artisan make:model Modelo -m
```

_`-m` para crear la migración_
_`-f` para crear la factoria_
_``$fillable`` nombre de las columnas_
```php
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

### softDelete
_migración_
```php
$table->softDeletes();
```

_modelo `app/Model.php`_
```php
use Illuminate\Database\Eloquent\SoftDeletes;
```
```php
class Modelo extends Model
{
    use SoftDeletes;
}
```

### Relaciones
#### Uno a uno
_Una relación de uno a uno es una relación muy sencilla. Por ejemplo, un modelo User podría estar asociado con un Phone. Para definir esta relación, colocaremos un método phone en el modelo User. El método phone debería llamar al método hasOne y devolver su resultado:_
```php
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class User extends Model
    {
        /**
        * Get the phone record associated with the user.
        */
        public function phone()
        {
            return $this->hasOne(Phone::class);
        }
    }
```
##### Definiendo el inverso de la relación
_Así, podemos acceder al modelo Phone desde nuestro User. Ahora, vamos a definir una relación en el modelo Phone que nos permitirá accdeder al User que posee el teléfono. Podemos definir el inverso de una relación hasOne usando el método belongsTo:_
```php
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Phone extends Model
    {
        /**
        * Get the user that owns the phone.
        */
        public function user()
        {
            return $this->belongsTo(User::class);
        }
    }
```
#### Uno a muchos
_Una relación de "uno-a-muchos" es usada para definir relaciones donde un solo modelo posee cualquier cantidad de otros modelos. Por ejemplo, un post de un blog puede tener un número infinito de comentarios. Al igual que todas las demás relaciones de Eloquent, las relaciones uno-a-muchos son definidas al colocar una función en tu modelo Eloquent:_
```php
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Post extends Model
    {
        /**
        * Get the comments for the blog post.
        */
        public function comments()
        {
            return $this->hasMany(Comment::class);
        }
    }
```
##### Uno a muchos (inverso)
_Ahora que puedes acceder a todos los comentarios de un post, vamos a definir una relación para permitir a un comentario acceder a su post padre. Para definir el inverso de una relación hasMany, define una función de relación en el modelo hijo que ejecute el método belongsTo:_
```php
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Comment extends Model
    {
        /**
        * Get the post that owns the comment.
        */
        public function post()
        {
            return $this->belongsTo(Post::class);
        }
    }
```
#### Muchos a muchos
_Las relaciones de muchos-a-muchos son definidas escribiendo un método que devuelve el resultado del método belongsToMany. Por ejemplo, vamos a definir el método roles en nuestro modelo User:_
```php
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class User extends Model
    {
        /**
        * The roles that belong to the user.
        */
        public function roles()
        {
            return $this->belongsToMany('App\Role');
        }
    }
```
##### Definiendo el inverso de la relación
_Para definir el inverso de una relación de muchos-a-muchos, puedes colocar otra llamada de belongsToMany en tu modelo relacionado. Para continuar con nuestro ejemplo de roles de usuario, vamos a definir el método users en el modelo Role:_
```php
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Role extends Model
    {
        /**
        * The users that belong to the role.
        */
        public function users()
        {
            return $this->belongsToMany('App\User');
        }
    }
```