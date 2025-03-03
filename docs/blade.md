# Blade en Laravel

Blade es el sistema de plantillas que Laravel utiliza para definir vistas. Permite realizar operaciones como sustitución de variables, herencia entre plantillas, definición de layouts y más.

- Los archivos Blade tienen la extensión `.blade.php`
- Para referenciar una vista que usa Blade no es necesario indicar la extensión:
    - `"home.blade.php"` → `view('home');`

## Sintaxis básica

### Comentarios

Los comentarios en Blade no se muestran en el HTML:

```blade
{{-- Este comentario no se mostrará en HTML --}}
```

### Mostrar valores

Para mostrar datos utilizamos llaves dobles:

```blade
Hola {{ $name }}
La hora actual es {{ time() }}
```

!!! warning "Escape de datos"
        Por defecto, los datos son escapados para prevenir ataques XSS.
        Si no quieres escapar los datos (usar con precaución):
        ```blade
        Hola {!! $name !!}
        ```

### Operador ternario

```blade
{{ isset($name) ? $name : 'Default' }}
```

O usando el operador de coalescencia nula:

```blade
{{ $name ?? 'Default' }}
```

## Estructuras de control

### Condicionales

#### If

```blade
@if(count($users) === 1)
        Solo hay un usuario!
@elseif(count($users) > 1)
        Hay muchos usuarios!
@else
        No hay ningún usuario :(
@endif
```

#### Unless (a menos que)

```blade
@unless(Auth::check())
        Usuario no identificado
@endunless
```

### Bucles

#### For

```blade
@for($i = 0; $i < 10; $i++)
        El valor actual es {{ $i }}
@endfor
```

#### While

```blade
@while(true)
        <p>Soy un bucle while infinito!</p>
@endwhile
```

!!! tip
        Dentro de un bucle puedes usar `@continue` y `@break` para controlar la ejecución.

#### Foreach

Itera sobre una colección de elementos:

```blade
@foreach($users as $user)
        <p>Usuario {{ $user->id }}</p>
@endforeach
```

#### Forelse

Similar a foreach pero con un caso especial para colecciones vacías:

```blade
@forelse($users as $user)
        <li>{{ $user->name }}</li>
@empty
        <p>No hay usuarios</p>
@endforelse
```

## Reutilización de código

### Sub-vistas

Incluir una plantilla dentro de otra:

```blade
@include('view_name')

{{-- Con datos adicionales --}}
@include('view_name', ['variable' => 'valor'])
```

### Componentes

Los componentes son sub-vistas parametrizables ubicadas en `/resources/views/components`:

```blade
<!-- /resources/views/components/alert.blade.php -->
<div class="alert alert-danger">
        {{ $slot }}
</div>
```

Para usar un componente:

```blade
<x-alert>
        <strong>Whoops!</strong> Something went wrong!
</x-alert>
```

#### Slots con nombre

Puedes definir slots adicionales en tus componentes:

```blade
<!-- /resources/views/components/alert.blade.php -->
<div class="alert alert-danger">
        <div class="alert-title">{{ $title }}</div>
        {{ $slot }}
</div>
```

Para asignarles valor:

```blade
<x-alert>
        <x-slot name="title">
                Forbidden
        </x-slot>
        You are not allowed to access this resource!
</x-alert>
```

## Layouts

### Definición de layout

```blade
<!-- /resources/views/layouts/master.blade.php -->
<html>
<head>
        <title>@yield('title')</title>
</head>
<body>
        @section('menu')
                Contenido del menu
        @show
        
        <div class="container">
                @yield('content')
        </div>
</body>
</html>
```

### Extender un layout

```blade
@extends('layouts.master')

@section('title', 'Título de la página')

@section('menu')
        @parent
        <p>Este contenido es añadido al menú principal.</p>
@endsection

@section('content')
        <p>Este apartado aparecerá en la sección "content".</p>
@endsection
```