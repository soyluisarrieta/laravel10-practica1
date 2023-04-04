# Mis apuntes

Autor del curso: [Victor Arana de Coders Free](https://codersfree.com/cursos/aprende-laravel-desde-cero)

## Instalaciones previas

1. XAMPP con PHP v8.2
2. Composer
3. NodeJS
4. Git
5. Visual Studio Code
6. Extensiones:
   1. "Laravel Snipperts" por WinnieLin
   2. "Laravel Blade formatter" por Shuhei Hayashibara
   3. "Laravel Blade Snippets" por Winnie Lin
   4. "Laravel goto view" por codingyu
   5. PHP intelephense

## Laravel

### Crear nuevo proyecto

Via Composer

```bash
composer create-project laravel/laravel example-app
```

Via Laravel primero se debe configurar el comando `laravel` para el proyecto

```bash
composer global require laravel/installer

laravel new example-app
```

El comando `laravel new example-app` es una opción más rápida y sencilla, ya que el instalador de Laravel utilizará Composer internamente para descargar e instalar Laravel y sus dependencias.

### Rutas

Retornar cadenas

```php
Route::get('/', function () {
  return "Hola mundo";
});
```

#### Rutas estáticas

```php
Route::get('/cursos/create', function () {
  return "Esta es la vista crear un curso";
});
```

#### Rutas dinámicas

```php
Route::get('/cursos/{curso}', function ($curso) {
  return "Bienvenido al curso $curso";
});
```

#### Rutas dinámicas anidadas y opcionales

```php
Route::get('/cursos/{curso}/{categoria?}', function ($curso, $categoria = null) {
  if($categoria){
    return "Bienvenido al curso $curso de la categoría $categoria";
  } else {
    return "Bienvenido al curso $curso";
  }
});
```

El orden en el que se definen las rutas en Laravel es importante, especialmente cuando se usan rutas dinámicas con parámetros. Es necesario definir primero las rutas estáticas antes de las dinámicas para evitar que Laravel confunda una ruta estática con un parámetro de ruta.

#### Rutas con controlador

Previamente se debe crear el controlador. La siguiente ruta llamará el método `__invoke`

```php
use App\Http\Controllers\HomeController;

Route::get('/', HomeController::class);
```

#### Rutas especificando un método

```php
use App\Http\Controllers\CursosController;

Route::get('/cursos/create', [CursosController::class, 'create']);
```

#### Grupo de rutas

Son rutas que comparten un mismo controlador pero con diferentes métodos

```php
Route::controller(CursoController::class)->group(function () {
  Route::get('/cursos', 'index');
  Route::get('/cursos/create', 'create');
  Route::get('/cursos/{curso}', 'show');
});
```

### Controladores

#### Crear un controlador desde la terminal

```bash
php artisan make:controller HomeController
```

El controlador se crea vacío pero si sólo se va administrar una única ruta, se puede crear el método `__invoke` que es ejecutado por una ruta :

```php
class HomeController extends Controller
{
  public function __invoke()
  {
    return "Esta es la página principal";
  }
}
```
