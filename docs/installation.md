# Creación de un Proyecto Laravel

## Nuevo Proyecto
Para crear un nuevo proyecto Laravel 11:
```
composer create-project laravel/laravel=11.* miproyecto --prefer-dist
```

## Configuración Inicial
1. Edita el archivo `.env`:
    ```
    SESSION_DRIVER=file
    ```

## Ejecución del Proyecto
Para iniciar el servidor de desarrollo:
```bash
php artisan serve
```

> **Nota**: Este comando iniciará un servidor local en `http://localhost:8000`
