# Migraciones en Laravel
## Inicialización de Base de Datos
```bash
php artisan migrate:install
```

## Creación de Migraciones

### Nueva Tabla
Para crear una migración de una nueva tabla:
```bash
php artisan make:migration create_products_table --create=products
```
Esto creará un archivo en: `database/migrations/<TIMESTAMP>_create_products_table.php`

### Modificar Tabla Existente
Para modificar una tabla existente:
```bash
php artisan make:migration add_price_to_products_table --table=products
```

## Gestión de Migraciones

### Ejecutar Migraciones
```bash
php artisan migrate
```

### Deshacer Migraciones
```bash
# Deshacer última migración
php artisan migrate:rollback

# Deshacer todas las migraciones
php artisan migrate:reset

# Deshacer y reejecutar todas las migraciones
php artisan migrate:refresh
```

### Estado de Migraciones
Para verificar el estado actual:
```bash
php artisan migrate:status
```

## Definición de Campos en Base de Datos

### Tipos de Campos Básicos

| Comando Laravel | Equivalencia en Base de Datos |
|----------------|------------------------------|
| `$table->id();` | Autoincremental UNSIGNED BIGINT (clave primaria) |
| `$table->unsignedBigInteger('votes');` | UNSIGNED BIGINT (usado para claves ajenas) |
| `$table->boolean('confirmed');` | BOOLEAN |
| `$table->date('created_at');` | DATE |
| `$table->dateTime('created_at', 0);` | DATETIME con precisión opcional |
| `$table->double('amount', 8, 2);` | DOUBLE con precisión y escala |
| `$table->float('amount', 8, 2);` | FLOAT con precisión y escala |
| `$table->integer('votes');` | INTEGER |
| `$table->string('name', 100);` | VARCHAR con longitud opcional |
| `$table->text('description');` | TEXT |
| `$table->time('sunrise', 0);` | TIME con precisión opcional |
| `$table->timestamp('added_on', 0);` | TIMESTAMP con precisión opcional |

### Modificadores de Campos
- `->nullable($value = true)`: Permite valores NULL
- `->default($value)`: Especifica valor por defecto

> **Nota**: Los campos son obligatorios por defecto a menos que se especifique `nullable()`

### Índices
Para añadir índices a los campos:
```php
$table->primary('id');                  // Clave primaria
$table->primary(['first', 'last']);     // Primaria compuesta
$table->unique('email');                // Campo único
$table->index('state');                 // Índice simple
$table->string('email')->unique();      // Índice al crear campo
```

### Claves Foráneas
Para crear relaciones entre tablas:
```php
$table->foreignId('user_id')->constrained();

// Con opciones adicionales
$table->foreignId('user_id')->constrained()
    ->cascadeOnDelete();

// Eliminar clave foránea
$table->dropForeign(['user_id']);
```
