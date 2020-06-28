# bv-flash
This is a Bootstrap Vue edition of a popular function I always use for forms and general actions.

## Install

Can be installed with `import` or `require`, here is an example using `require`:

    Vue.use(require('BvFlash'));

## Usage

All this plugin does is receive events on the `$root` `Vue` element and send them to a component in your layout.

For example, a layout in Laravel's blade templates:
```blade
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
</head>
<body>
    <div id="app">
        <nav class="navbar navbar-expand-md navbar-light bg-light fixed-top">
        </nav>
        <div class="body-fixed-top @yield('container')">
            @include('flash::flash', ['class' => 'mb-0 alert-sticky-flash'])
            <bv-flash-component></bv-flash-component>
            <main class="">
                @yield('content')
            </main>
        </div>
    </div>
</body>
</html>
```
`bv-flash-component` being the registered plugin component, in a component:

    this.$root.$emit('bv-flash::show', 'OMG couldn\'t save', 'danger');
    
This will make this message `"OMG couldn't save"` show at the top of your page just under the site navigation.

`$emit()` takes two parameters, the message and the type. The type relates to the types you will find in the documentation, for example: `info`, `success`, `light`, `dark`, and more.

## Notes

This plugin, unlike other plugins like it, does not have a helper class with its own event bus, I chose to stay away from that pattern and observe the pattern I love most: KISS. This will use one `Vue` instance, the `$root` one, no creating multiple nested instances. 
