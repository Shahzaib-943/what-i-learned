# Installing Vue.js with Inertia Manually



## Steps

### Server-side configuration

#### Step 1: Install inertia with following command


```bash
composer require inertiajs/inertia-laravel
```

#### Step 2: Make a layout file in resources/app.blade.php., like this, if already no starter kit with scaffolding (breeze, jetstream, etc) is made.


```bash
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    @vite('resources/js/app.js')
    @inertiaHead
  </head>
  <body>
    @inertia
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
  </body>
</html>

```

Paste all the bootstrap CDN, etc here (In above code, CDNs are placed).

#### Step 3: Make Inertia middleware, with this command


```bash
php artisan inertia:middleware
```

#### Step 4: Register the middleware in kernal.php file in web group middlewares.


```bash
\App\Http\Middleware\HandleInertiaRequests::class,
```

#### Step 5: Register the middleware in kernal.php file in web group middlewares.


```bash
\App\Http\Middleware\HandleInertiaRequests::class,
```

### Client-side configuration

#### Step 6: Install Inertia/VueJS Adapter.


```bash
npm install @inertiajs/vue3
```

#### Step 7: Install vue (if not already).


```bash
npm install vue@next
```
or
```
npm install vue@latest
```

#### Step 8: Install vitejs plugin.


```
npm install @vitejs/plugin-vue
```
#### Step 9: Configure Vuejs in vite.config.js, like this


```
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        vue({
            template: {
                transformAssetUrls: {
                    base: null,
                    includeAbsolute: false,
                }
            },
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});

```

#### Step 10: Add this code in resources/js/app.js

```
import { createApp, h } from 'vue'
import { createInertiaApp } from '@inertiajs/vue3'

createInertiaApp({
  resolve: name => {
    const pages = import.meta.glob('./Pages/**/*.vue', { eager: true })
    return pages[`./Pages/${name}.vue`]
  },
  setup({ el, App, props, plugin }) {
    createApp({ render: () => h(App, props) })
      .use(plugin)
      .mount(el)
  },
})
```

#### Step 11: Make a new folder in resources/js/Pages, and make all vue files here, e.g,

resources/js/Pages/Index.vue
