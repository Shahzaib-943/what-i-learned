# Using Laravel Named Routes in Inertia VueJs Projecr
We can use Laravel named routes in our inertia vue project by using a package known as "ziggy" by "tighten"


## Steps



#### Step 1: Install ziggy with following command


```bash
composer require tightenco/ziggy
```

#### Step 2: Add "routes()" before the JS directive directive in main layout file (app.blade.php, in my case).


```bash
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    @vite('resources/js/app.js')

    @routes()

    @inertiaHead
</head>

<body>
    @inertia
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous">
    </script>
</body>

</html>
```


#### Step 3: Import ZiggyVue and use it in main app.js file, like this


```bash
import './bootstrap';

import { createApp, h } from 'vue'
import { createInertiaApp } from '@inertiajs/vue3'
import { ZiggyVue } from '../../vendor/tightenco/ziggy'

createInertiaApp({
  resolve: name => {
    const pages = import.meta.glob('./Pages/**/*.vue', { eager: true })
    return pages[`./Pages/${name}.vue`]
  },
  setup({ el, App, props, plugin }) {
    createApp({ render: () => h(App, props) })
        .use(plugin)
        .use(ZiggyVue)
      .mount(el)
  },
})
```

#### Step 4: Now, you can the named routes in href like this,


```bash
<Link class="nav-link" :href="route('skills.index')">Skills</Link>
```

You are all good to go...

## Author

[@Shahzaib](https://github.com/Shahzaib-943)
