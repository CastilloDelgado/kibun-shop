# Kibun Shop

Base para una tienda en línea propia con Laravel 12, Vue 3, TypeScript, Inertia 2, Tailwind CSS y Vite. Incluye autenticación y ajustes de perfil del starter oficial. Catálogo, carrito, pedidos y pagos quedan pendientes de implementar.

## Requisitos

- PHP 8.2 o superior con PDO SQLite y las extensiones requeridas por Laravel.
- Composer 2.
- Node.js 22.17 o superior y npm.

## Desarrollo local

La instalación inicial ya está preparada. Para iniciar:

```sh
composer run dev
```

Abre http://localhost:8000. Detén los procesos con Ctrl+C.

Para instalar desde un clon nuevo:

```sh
composer install
cp .env.example .env
php artisan key:generate
php -r "file_exists('database/database.sqlite') || touch('database/database.sqlite');"
php artisan migrate
npm ci
npm run build
composer run dev
```

SQLite permite comenzar sin instalar otro servidor de base de datos. Los correos se escriben en el registro local (`MAIL_MAILER=log`); se necesita un proveedor de correo antes de producción. La interfaz de autenticación conserva los textos en inglés del starter.

## Verificación

```sh
php artisan test
npm run build
npx vue-tsc --noEmit
```

## Estructura

- `app/`: lógica del servidor y modelos.
- `routes/`: rutas web y autenticación.
- `resources/js/pages/`: páginas Vue.
- `resources/js/components/`: componentes reutilizables.
- `database/migrations/`: estructura de la base de datos.

## GitHub

La rama principal es `main`. Si el remoto aún no existe, crea un repositorio privado vacío llamado `kibun-shop` en tu cuenta de GitHub y ejecuta:

```sh
git remote add origin git@github.com:CastilloDelgado/kibun-shop.git
git push -u origin main
```

Esto requiere que tu equipo tenga acceso SSH a GitHub. También puedes usar la URL HTTPS que proporciona GitHub.

## Alojamiento

El proyecto no depende de un proveedor: se puede desplegar en un VPS o AWS. Antes de producción hay que configurar el servidor web con raíz en `public/`, HTTPS, base de datos y respaldos, correo, un proceso de colas y las variables del entorno (`APP_ENV=production`, `APP_DEBUG=false`, `APP_URL` real). Compila con `npm ci && npm run build` e instala las dependencias PHP sin desarrollo.

No subas `.env`, credenciales, dependencias ni la base de datos local: ya están excluidos por Git. Las comisiones de la pasarela de pagos y los costos de infraestructura dependerán de los servicios elegidos.

Base: [starter oficial de Laravel con Vue](https://laravel.com/docs/starter-kits#vue).

## Dependencias

Se aplicaron actualizaciones compatibles de npm. La última auditoría reportó 14 avisos (1 bajo y 13 moderados), sin avisos altos ni críticos. Revisa `npm audit` antes del despliegue; algunas correcciones requieren cambiar versiones mayores.
