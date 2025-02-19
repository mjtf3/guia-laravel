# Gestión de Registros (Logging) en Laravel

Laravel integra la librería [Monolog](https://github.com/Seldaek/monolog) para la gestión de archivos de registro (logs).

## Documentación Oficial

Consulta la [documentación de Laravel](https://laravel.com/docs/11.x/logging) para más detalles sobre la configuración y el uso de logging.

## Uso de Monolog

Monolog permite imprimir mensajes que se almacenarán en el archivo de registro, ubicado por defecto en `storage/logs/laravel.log`.

### Niveles de Importancia

Los mensajes pueden tener distintos niveles de importancia, de menor a mayor:

- **debug**
- **info**
- **notice**
- **warning**
- **error**
- **critical**
- **alert**
- **emergency**

> Nota: Sólo se guardarán en el log aquellos mensajes cuyo nivel de importancia sea mayor o igual al especificado en el fichero `config/logging.php`.

## Ejemplo de Uso

Para utilizar Monolog, es necesario incluir la clase `Log`:

```php
use Illuminate\Support\Facades\Log;
```

La clase ofrece métodos estáticos que se corresponden con los niveles de importancia. Por ejemplo:

```php
Log::debug("Debug message");
Log::warning("This is a warning");
```