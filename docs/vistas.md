# Vistas en Laravel

Las vistas en Laravel:
- Presentan el resultado de forma visual al usuario, permitiendo interacción
- Separan la presentación de resultados de la lógica (controladores) y base de datos (modelos)
- No realizan consultas ni procesan datos, solo reciben y muestran información
- Se almacenan en la carpeta `resources/views` como ficheros PHP

## Contenido de las vistas

Pueden contener:
- Código HTML
- Assets (CSS, imágenes, JavaScript, etc. que estarán en la carpeta `public`)
- Código PHP (o plantillas con Blade) para presentar datos como resultado HTML

## Vistas sin Blade

Ejemplo de vista guardada en `resources/views/home.php`:

```html
<html>
<head>
    <title>Mi Web</title>
</head>
<body>
    <h1>¡Hola <?php echo $name; ?>!</h1>
</body>
</html>
```

Para asociarla con una ruta, en el fichero `routes/web.php` añadimos:

```php
Route::get('/', function() {
    return view('home', ['name' => 'John']);
});
```

## Pasar parámetros a vistas

Al construir una vista podemos pasarle parámetros de varias formas:

```php
view('home', ['name' => 'Pedro', 'age' => 18]);
view('home')->with('name', 'Javi')->with('age', 18);
```

## Vistas en subcarpetas

Para hacer referencia a una vista en una subcarpeta:
- `"resources/views/user/profile"` → `"user.profile"`

Por ejemplo:

```php
Route::get('user/profile/{id}', function($id) {
    $user = // Cargar usuario a partir de $id
    return view('user.profile', ['user' => $user]);
});
```