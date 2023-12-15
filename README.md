### Alquiler de Autos

**Iniciando el proyecto**

```shell
composer create-project --prefer-dist laravel/laravel app_locadora_carros "8.5.9"
composer create-project --prefer-dist laravel/laravel=8.5.9 app_locadora_carros
```

[packagist.org](https://packagist.org/packages/laravel/laravel)

```shell
cd app_locadora_carros
```

```php
php artisan serve
```

**Creando los modelos, controladores y migraciones**

Marca
```php
php artisan make:model --migration --controller --resource Marca
```

Modelo
```php
php artisan make:model -mcr Modelo
```

Carro
```php
php artisan make:model --all Carro
```

Cliente
```php
php artisan make:model -a Cliente
```

Locación
```php
php artisan make:model -a Locacion
```

**Configurando la conexión a la base de datos e implementando las migraciones**

```sql
CREATE DATABASE lc;
```

```php
php artisan migrate
```

**Comprendiendo el grupo de rutas Web y API y la importancia del Content-Type**
- Respuesta
    - Cabeceras
        - Content-Type
            - text/html
            - application/json

```
http://127.0.0.1:8000/api/
```

**Rutas y la diferencia entre Route::resource y Route::apiResource**

```php
php artisan route:list
```

**Creando registros mediante POST**

```sql
USE LC;
DESCRIBE marcas;
SELECT * FROM marcas;
```

**Actualizando registros mediante PUT y PATCH**
- PUT se utiliza para actualizar todos los campos.
- PATCH se utiliza para actualizar un campo específico.

**Comprendiendo el concepto de punto final (URL, URN y URI)**
- URL - Localizador de Recursos Uniforme
    - Host donde se encuentra el recurso.
- URN - Nombre de Recurso Uniforme
    - Recurso dentro del host.
- URI - Identificador de Recurso Uniforme
    - Combinación del protocolo + URL + URN

**Validaciones parte 3 - Validando parámetros y la importancia del Accept**
- Cabeceras
    - Content-Type | application/x-www-form-urlencoded
    - Accept | application/json

**Validaciones parte 4 - Reglas de validación en la actualización - Manejando Unique**
- Unique
    - 1) Tabla
    - 2) Nombre de la columna que se buscará en la tabla
    - 3) ID del registro que se omitirá en la búsqueda

**Carga de archivos - Implementando la carga de imágenes parte 1**

```php
$request->nombre;
$request->get('nombre');
$request->input('nombre');

$request->imagen;
$request->file('imagen');
```

**Implementando la carga de imágenes parte 2**
- Disco - config/filesystems.php
    - local -> /storage/app/
    - public -> /storage/app/public/
    - AWS S3 -> cloud

**Implementando la carga de imágenes parte 3**

```php
$marca = $this->marca->create([
    'nombre' => $request->nombre,
    'imagen' => $imagen_urn
]);

$marca->nombre = $request->nombre;
$marca->imagen = $imagen_urn;
$marca->save();
```

**Carga de archivos - Creando un enlace simbólico para el disco público**

```php
php artisan storage:link
```

**Carga de archivos - Actualizando imágenes**

POST - form-data
```
nombre        BMW - Prueba
imagen        ford.png
_method       put
```

---

**Instalando el paquete JWT-Auth**

```
composer require tymon/jwt-auth "1.0.2"
```

**Configurando JWT-Auth en el proyecto**

[jwt-auth](https://jwt-auth.readthedocs.io/en/develop/laravel-installation/)

config/app.php
```
'providers' => [
    ...
    Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
]
```

config/jwt.php
```
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
```

.env: JWT_SECRET=foobar
```
php artisan jwt:secret
```

**Creando rutas de autenticación y autorización y el AuthController**

```php
php artisan make:controller AuthController
```

**Insertando un usuario en la base de datos**

```php
php artisan tinker

$user = new App\Models\User();

$user->name = 'Lucas';
$user->email = 'lucasdarosa.ti@gmail.com';
$user->password = bcrypt('1234');

$user->save();
```

---

**Agregando la relación entre modelos y marcas**

- all()
    - Crea un objeto de consulta + get() = Colección
- get()
    - Modificar la consulta - Colección

---

**Expiración de JWT por tiempo límite**

```
JWT_TTL=120 // minutos en el archivo .env
```

---

**Configurando Vue.JS en Laravel**

Instalar el paquete UI
```
composer require laravel/ui:^3.2.1
```

Generar el esqueleto del proyecto con Vue.JS y autenticación web nativa (scaffold / esqueleto)
```php
php artisan ui vue --auth
```

Instalar las dependencias de frontend
```
npm install
```

Cargador de Vue
```
npm install vue-loader@^15.9.8 --save-dev --legacy-peer-deps
```

Generar el paquete de frontend
```
npm run dev
```

**Instalando y configurando Vuex en el proyecto**

```
npm install vuex@3.6.2
```
