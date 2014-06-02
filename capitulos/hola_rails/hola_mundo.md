Hola Mundo
==========

Para conseguir que Rails diga "Hola", necesitas crear como mínimo un _controlador_ y
una _vista_.

El propósito de un controlador es recibir peticiones específicas (requests) de la
aplicación. El enrutamiento (_Routing_) decide qué controlador recibe qué petición.
A menudo, hay más de una ruta para cada controlador, y diferentes rutas pueden
ser servidas por diferentes acciones (_actions_). El propósito de cada acción
es recolectar información para posteriormente brindarla a la vista.

El propósito de una vista es mostrar la información en un formato legible para
los humanos. Una distinción importante que hacer es que es el _controlador_, y
no la vista, donde la información es recolectada. La vista sólo debería mostrar
la información. Por defecto, las plantillas de las vistas están escritas en un
lenguaje llamado _ERB_ (Embedded Ruby), el cual es convertido por cada ciclo
de un request en Rails antes de ser enviado al usuario.

Para crear un nuevo controlador, necesitas correr el generador de controladores
y decirle que quieres un controlador llamado "welcome" con una acción llamada
"index", casi como lo siguiente:

```bash
$ rails generate controller welcome index
```

Rails creará una serie de archivos y añadirá una ruta por ti.

```bash
create  app/controllers/welcome_controller.rb
 route  get "welcome/index"
invoke  erb
create    app/views/welcome
create    app/views/welcome/index.html.erb
invoke  test_unit
create    test/functional/welcome_controller_test.rb
invoke  helper
create    app/helpers/welcome_helper.rb
invoke    test_unit
create      test/unit/helpers/welcome_helper_test.rb
invoke  assets
invoke    coffee
create      app/assets/javascripts/welcome.js.coffee
invoke    scss
create      app/assets/stylesheets/welcome.css.scss
```

Los más importantes de éstos son por supuesto el controlador, localizado en
`app/controllers/welcome_controller.rb` y la vista, localizada en
`app/views/welcome/index.html.erb`.

Abre el archivo `app/views/welcome/index.html.erb` en tu editor de texto
y edítalo para que contenga sólo está línea de código:

```html
<h1>Hello, Rails!</h1>
```
