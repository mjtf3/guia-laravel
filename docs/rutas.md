# Rutas en Laravel

Las rutas de la aplicación se definen en los siguientes ficheros:

**Directorio `routes/`:**
- `api.php` → Rutas para API
- `channels.php` → Suscripciones a eventos
- `console.php` → Rutas para consola
- `web.php` → Rutas para acceso Web

> **Nota**: Cualquier ruta no definida retornará un error 404.

## Definición de rutas

Para cada ruta se define:
- Método HTTP de la petición: `GET`, `POST`, `PUT`, `DELETE`
- Ruta URL (sin el dominio, que está definido en `config/app.php`)
- Respuesta a la petición a esa ruta

Podemos devolver tres tipos de respuestas:
- Un valor (como una cadena)
- Una vista
- Enlazar con un método de un controlador

## Ejemplos básicos

Ejemplo de ruta para peticiones tipo GET a la URL raíz:

```php
Route::get('/', function() {
    return '¡Hola mundo!';
});
```

Ejemplo de respuesta a peticiones tipo POST:

```php
Route::post('foo/bar', function() {
    return '¡Hola mundo!';
});
```

## Múltiples métodos HTTP

Definir una ruta que responda a varios tipos de peticiones:

```php
Route::match(['GET', 'POST'], '/', function() {
    return '¡Hola mundo!';
});
```

O que responda a todos los métodos HTTP:

```php
Route::any('foo', function() {
    return '¡Hola mundo!';
});
```

## Parámetros en rutas

Para añadir parámetros a las rutas, se indican entre llaves `{}`:

```php
Route::get('user/{id}', function($id) {
    return 'User ' . $id;
});
```

Si queremos parámetros opcionales, añadimos el símbolo `?`:

```php
Route::get('user/{name?}', function($name = null) {
    return $name;
});
```

Para generar un enlace a una ruta:

```php
$url = url('foo');
```

## Rutas con nombre

Podemos asignar nombre a las rutas:

```php
Route::get('user/{id}', function($id) {
    // Lógica
})->name('user.show');
```

Se puede generar un enlace a una ruta usando su nombre:

```php
$url = route('user.show', ['id' => 1]);
```