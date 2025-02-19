# Pruebas Automatizadas en Laravel

## Introducción
Laravel ofrece soporte integrado para pruebas automatizadas mediante PHPUnit. Este documento muestra cómo organizar y crear pruebas en tu aplicación Laravel.

## Organización de las Pruebas
Las pruebas se ubican en la carpeta `tests` y se dividen en dos categorías:

- **Unit**: Pruebas unitarias para métodos y funciones individuales.
- **Feature**: Pruebas que evalúan la interacción entre componentes.

Consulta la [documentación oficial de pruebas en Laravel](https://laravel.com/docs/11.x/testing) para obtener más detalles.

## Creación de Tests
Genera tests utilizando Artisan:

- Para crear un test en la carpeta Feature:
    ```
    php artisan make:test UserTest
    ```

- Para crear un test en la carpeta Unit:
    ```
    php artisan make:test UserTest --unit
    ```

## Uso de Aserciones
Las pruebas se basan en aserciones que verifican el comportamiento esperado del código. Revisa las [aserciones de PHPUnit](https://docs.phpunit.de/en/11.5/assertions.html) para más información.

### Ejemplo de Prueba
```php
class MathTest extends TestCase
{
    public function testExample()
    {
        $this->assertEquals(4, Math::sum(2, 2));
    }
}
```

## Ejecución de Tests
Para ejecutar los tests, puedes utilizar uno de los siguientes comandos:

- Usando Artisan (recomendado en Laravel):
    ```
    php artisan test
    ```

- Usando PHPUnit directamente:
    ```
    ./vendor/bin/phpunit
    ```