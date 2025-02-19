# Seeders de Base de Datos

# Database Seeding

Los seeders de base de datos permiten insertar datos iniciales de prueba en tu base de datos. Esto es particularmente útil para:

- Pruebas de desarrollo
- Pre-poblar tablas que requieren datos iniciales

## Ubicación y Estructura

Los seeders se almacenan en el directorio `database/seeds`. El método `run` de la clase `DatabaseSeeder` es el punto de entrada, desde donde puedes:

- Ejecutar métodos privados dentro de la clase
- Llamar a otros archivos/clases de seeders

## Comandos Artisan Disponibles

Puedes utilizar los siguientes comandos para trabajar con seeders:

```bash
# Crear un nuevo seeder
php artisan make:seeder UsersTableSeeder

# Ejecutar todos los seeders
php artisan db:seed

# Refrescar la base de datos y sembrar
php artisan migrate:refresh --seed
```

## Ejemplos de Implementación

### La Clase DatabaseSeeder

```php
class DatabaseSeeder extends Seeder 
{
    public function run() 
    {
        // Llamar a otro archivo seeder
        $this->call(UserTableSeeder::class);
        
        // Mostrar información en la consola
        $this->command->info('¡Tabla de usuarios sembrada!');
    }
}
```

### Implementación del UserTableSeeder

```php
class UsersTableSeeder extends Seeder 
{
    public function run() 
    {
        // Limpiar la tabla de usuarios
        DB::table('users')->delete();
        
        // Insertar un nuevo registro
        DB::table('users')->insert([
            'name' => 'NombreUsuario',
            'email' => 'nombre@dominio.com',
            'password' => 'contraseñasegura'
        ]);
        
        // Nota: usa el método insertGetId() para obtener el ID asignado
    }
}
```

## Query Builder

Laravel proporciona un conjunto robusto de herramientas para interactuar con tu base de datos:

### Características Principales

- Compatible con múltiples bases de datos soportadas por Laravel
- Sintaxis clara y legible
- Protección contra inyección SQL

### Uso Básico

```php
use Illuminate\Support\Facades\DB;

// Consulta básica
$users = DB::table('users')->get();

// Iterar resultados
foreach($users as $user) {
    echo $user->name;
}
```

### Métodos Comunes

```php
// Obtener un único registro
$user = DB::table('users')->where('name', 'John')->first();

// Ordenar y agrupar resultados
$users = DB::table('users')
    ->orderBy('name', 'desc')
    ->groupBy('count')
    ->having('count', '>', 100)
    ->get();
```

> **Nota**: Para más información sobre operaciones adicionales como join, insert, update, delete, consulta la [documentación oficial de Laravel](https://laravel.com/docs).
