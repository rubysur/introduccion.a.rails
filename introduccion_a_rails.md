Introducción a Rails
==========================

Esta guía cubre ¿cómo comenzar con Ruby on Rails? Luego de leerla, aprenderás
lo siguiente:

* Instalar Rails, crear una nueva aplicación Rails y conectar tu aplicación a
  una base de datos.
* La estructura general de una aplicación Rails.
* Los principios básicos del patrón MVC (Modelo, Vista, Controlador) y
  Diseño RESTful.
* Como generar rápidamente las primeras piezas de una aplicación Rails.

--------------------------------------------------------------------------------

WARNING. Esta guía está basada en Rails 4.0. Algunas partes del código que
se muestran aquí no van a funcionar en nuevas versiones de Rails.

Antes de Empezar
----------------

Esta guía está diseñada para principiantes que quieren comenzar con Rails
desde cero. No asume que tú tienes alguna experiencia previa con Rails. Sin,
embargo, para obtener el máximo de ésta, tú debes de tener algunos
pre-requisitos instalados:

* El lenguaje de programación [Ruby](http://www.ruby-lang.org/en/downloads) en
  su versión 1.9.3 o mayor.
* El sistema de paquetes [RubyGems]([RubyGems](http://rubyforge.org/frs/?group_id=126).
    * Si quieres aprender más acerca de RubyGems, puedes leer la guía en inglés:
      [RubyGems User Guide](http://docs.rubygems.org/read/book/1).
* La base de datos [SQLite3](http://www.sqlite.org).

Rails es un framework para aplicaciones web que corre sobre el lenguaje
de programación Ruby. Si no tienes ninguna experiencia con Ruby, existen
algunos recursos gratis en la internet para aprender Ruby, incluyendo:

* [Aprende a Programar con Ruby](http://aprendeaprogramar.pe/). *En español*.
* [Mr. Neighborly's Humble Little Ruby Book](http://www.humblelittlerubybook.com).
* [Programming Ruby](http://www.ruby-doc.org/docs/ProgrammingRuby/).
* [Why's (Poignant) Guide to Ruby](http://mislav.uniqpath.com/poignant-guide/).

¿Qué es Rails?
--------------

Rails es un framework de desarrollo de aplicaciones web escrito en el
lenguaje de programación Ruby. Está diseñado para hacer que la programación
de aplicaciones web sea más fácil, haciendo supuestos sobre lo que cada
desarrollador necesita para comenzar. It allows you to write less code while
accomplishing more than many other languages and frameworks. Además, expertos
desarrolladores en Rails reportan que hace que el desarrollo de aplicaciones
web sea más divertido.

Rails es un software dogmático. Éste asume que existe una forma "mejor" de hacer
las cosas, y está diseñado para fomentar esa forma - y en algunos casos para
desalentar alternativas. Si aprendes "El Modo Rails" probablemente descubrirás
un tremendo incremento en tu productividad. Si persistes trayendo viejos hábitos
de otros lenguajes a tu desarrollo en Rails, e intentas usar patrones aprendidos en
otros lugares, podrías tener una experiencia menos agradable.

La filosofía de Rails incluye dos mayores principios:

* DRY - "Don't Repeat Yourself" - sugiere que escribir el mismo código una y
  otra vez es una mala práctica.
* Convención sobre Configuración - significa que Rails hace algunas
  suposiciones sobre lo que tú quieres hacer y cómo vas a hacerlo, en lugar
  de requerir que especifiques cada pequeña cosa a través de un sin fin
  de archivos de configuración.

Creando un nuevo proyecto Rails
-------------------------------

La mejor forma de usar esta guía es seguir cada paso como es el caso, no hay
ningún código o paso para hacer este ejemplo de aplicación que haya quedado
fuera, así que puedes literalmente seguirla paso a paso. Puedes tener el código
completo [aquí](https://github.com/lifo/docrails/tree/master/guides/code/getting_started).

Al seguir esta guía, tú vas a crear un proyecto Rails llamado `blog`, un (muy)
simple weblog. Antes de que puedas comenzar a crear la aplicación, necesitas
estar seguro de tener Rails instalado.

TIP: Los ejemplos que se muestran a continuación usan `#` y `$` para denotar un
superuser y user regultar de una línea de comandos respectivamente en un sistema
operativo tipo UNIX. Si estás usando Windows, tú línea de comandos se verá como
`c:\source_code>`.

### Instalando Rails

Para instalar Rails, usa el comando proporcionado por RubyGems `gem install`:

```bash
# gem install rails
```

TIP. Existen un número de herramientas que te ayudarán a instalar Ruby y
Ruby on Rails de una manera rápida. Si eres usuario de Windows puedes usar
[Rails Installer](http://railsinstaller.org/). Si eres usuario de Mac OS X
puedes usar [Rails One Click](http://railsoneclick.com/).

Para verificar que tu instalación esté correcta, deberías
poder correr lo siguiente:

```bash
$ rails --version
```

Si dice algo como "Rails 4.0", estás listo para continuar.

### Creando la aplicación de Blog

Rails viene con un número de generadores que están diseñados para hacer tu ciclo
de desarrollo más fácil. Uno de esos es el generador de nuevas aplicaciones, el
cual te proveerá con la estructura base de una aplicación Rails, así ya no
tienes que escribirla por ti mismo.

Para usar este generador, abre la terminal, navega hacia el directorio en donde
tienes permiso para crear archivo, y escribe:

```bash
$ rails new blog
```

Esto creará una aplicación Rails llamada `Blog` en un directorio llamado `blog`
e instalará las dependencias (gemas) que están mencionadas en el `Gemfile` usando
el comando `bundle install`.

TIP: Puedes ver todas las opciones que el generador de nuevas aplicaciones
provee, ejecutando `rails new -h`.

Después de crear la aplicación, ingresa a su directorio para continuar trabajando
directamente en la aplicación:

```bash
$ cd blog
```

El comando `rails new blog` que acabamos de ejecutar, creó una carpeta en tu
directorio de trabajo llamado `blog`. El directorio `blog` tiene un número
de archivos auto generados y carpetas que conforman la estructura de una
aplicación Rails. La mayoría del trabajo en este tutorial se llevará a cabo en
la carpeta `app/`, pero acá hay una explicación básica de las funciones de
cada archivo y carpetas que Rails creó por defecto:

| Archivo/Carpeta | Propósito |
| --------------- | --------- |
|app/|Contiene los controllers, models, views, helpers, mailers y assets para tu aplicación. Te centrarás en esta carpeta por el resto de esta guía.|
|config/|Configura las reglas de ejecución de la aplicación, rutas, base de datos y más. Este tema es cubierto en mayor detalle en [Configuring Rails Applications](http://edgeguides.rubyonrails.org/configuring.html).|
|config.ru| Configuración Rack para servidores basados en Rack usados para iniciar la aplicación.|
|db/|Contiene el esquema actual de tu base de datos, así como las migraciones de la base de datos.|
|doc/|Documentación detallada de tu aplicación.|
|Gemfile<br />Gemfile.lock| Estos arhivos te permiten especificar que dependencias de gemas son necesitadas para tu aplicación Rails. Estos archivos son usados por la gema Bundler, ver [Sitio web de Bundler](http://gembundler.com).|
|lib/|Módulos extendidos para tu aplicación.|
|log/|Archivos de Log de tu aplicación.|
|public/|La única carpeta vista por el mundo tal como es. Contiene los archivos estáticos y assets compilados.|
|Rakefile|Este archivo localiza y carga tareas que pueden ser ejecutadas desde la línea de comandos. La lista de tareas son definidas a través de los componentes de Rails. En vez de cambiar el Rakefile, deberías agregar tus propias tareas, añadiendo archivos al directorio `lib/tasks` de tu aplicación.|
|README.rdoc|Este es un breve manual de instrucciones para tu aplicación. Deberías editar este archivo para comunicar a otros lo que tu aplicación hace, como configurala y demás.|
|script/|Contiene el script de Rails que inicia tu aplicación y contiene otros scripts usados para deployar o correr tu aplicación.|
|test/|Pruebas unitarias, fixtures y otras pruebas. Éstos son cubiertos en [Testing Rails Applications](http://edgeguides.rubyonrails.org/testing.html).|
|tmp/|Archivos temporales (como archivos de caché, pid y archivos de sesiones).|
|vendor/|Lugar para código de terceros. En una típica aplicación Rails, ésta incluye librerías y plugins.|

Hola, Rails!
------------

Para comenzar, vamos a obtener un poco de texto en la pantalla rápidamente. Para
hacer ésto, necesitas tener tu servidor de aplicación Rails corriendo.

### Iniciando el Servidor Web

En realidad ya tienes una aplicación Rails funcional, Para verla, necesitas
iniciar un servidor web en tu máquina de desarrollo. Puedes hacerlo ejecutando:

```bash
$ rails server
```

TIP: Compilando CoffeeScript a JavaScript requiere un JavaScript runtime y la
ausencia de éste dará un error de `execjs`. Usualmente Mac OS X y Windows vienen
con un Javascript runtime instalado. Rails agrega la gema `therubyracer` al
`Gemfile` en una línea comentada para nuevas aplicaciones y puedes descomentarla
si la necesitas. `therubyrhino` es el runtime recomendado para usuarios de JRuby
y es añadido por defecto al `Gemfile` en aplicaciones generadas bajo JRuby.
Puedes investigar acerca de todos los runtimes soportados en
[ExecJS](https://github.com/sstephenson/execjs#readme).

Esto lanzará WEBrick, un servidor web incoporado en Ruby por defecto. Para ver
tu aplicación en acción, abre tu navegador preferido e ingresa a la siguiente
dirección [http://localhost:3000](http://localhost:3000). Deberías ver la página
de información por defecto de Rails.

![Welcome Aboard screenshot](http://edgeguides.rubyonrails.org/images/rails_welcome.png)

TIP: Para detener el servidor web, presiona Ctrl+C en la ventana de la línea
de comandos donde se esta ejecutando. En modo de desarrollo, Rails generalmente
no requiere reiniciar el servidor web; los cambios realizados serán tomados
automáticamente por el servidor.

La página "Welcome Aboard" es la primera prueba para una nueva aplicación Rails:
Ésta asegura que tienes el software configurado correctamente para servir una página.
También puedes hacer click en el link _About your application's enviroment_ para ver
un resumen del entorno de tu aplicación.

### Say "Hello to my little friend", Rails

Para conseguir que Rails diga "Hola", necesitas crear como mínimo un _controlador_ y
una _vista_.

El propósito de un controlador es recibir peticiones específicas (requests) por la
aplicación. El enrutamiento (_Routing_) decide que controlador recibe que petición.
A menudo, hay más de una ruta para cada controlador, y diferentes rutas pueden
ser servidas por diferentes acciones (_actions_). Cada propósito de la acción
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
`app/controllers/welcome_controller.rb` y la vista, localizado en
`app/views/welcome/index.html.erb`.

Abre el archivo `app/views/welcome/index.html.erb` en tu editor de texto
y edítalo para que contenga sólo está línea de código:

```html
<h1>Hello, Rails!</h1>
```

### Estableciendo la página principal de la aplicación

Ahora que hemos hecho el _controlador_ y la _vista_, necesitamos decirle a Rails
cuando queremos que `Hello Rails` se muestre. En nuestro caso, deseamos mostrarlo
al ingresar a la raíz de nuestro sitio, <http://localhost:3000>. Por el momento,
sin embargo, la página "Welcome Aboard" está ocupando ese lugar.

Para arreglarlo, borra el archivo `index.html` ubicado dentro de la carpeta
`public` de la aplicación.

Necesitas hacer ésto debido a que Rails servirá cualquier archivo estático en la
carpeta `public` que coincida con una ruta, en preferencia a cualquier contenido
que puedas generar desde los _controladores_. El archivo `index.html` es
especial: éste será servido si una petición llega a la ruta raíz, por ejemplo
http://localhost:3000. Si otra petición tal como http://localhost:3000/welcome
ocurriera, un archivo estático en `public/welcome.html` sería servido primero,
pero sólo si existiera.

A continuación, tienes que indicarle a Rails donde está ubicada tu página principal.

Abre el archivo `config/routes` en tu editor.

```ruby
Blog::Application.routes.draw do
  get "welcome/index"

  # The priority is based upon order of creation:
  # first created -> highest priority.
  # ...
  # You can have the root of your site routed with "root"
  # just remember to delete public/index.html.
  # root :to => "welcome#index"
```

Éste es el _archivo de enrutamiento_ de tu aplicación el cual mantiene entradas
con un DSL especial (domain-specific language) que le dicen a Rails como conectar
peticiones entrantes a _controladores_ y _acciones_. Este archivo contiene muchas
rutas de ejemplo en líneas comentadas, y una de ellas en realidad muestra como
conectar la raíz de tu sitio a un _controlador_ y _acción_ específico. Encuentra
la línea iniciando con `root :to` y descoméntala. Debería verse como lo siguiente:

```ruby
root :to => "welcome#index"
```

El `root :to => "welcome#index"` le indica a Rails mapear peticiones de la raíz
de la aplicación a la _acción_ `index` del _controlador_ `welcome` y
`get "welcome/index"` le indica a Rails mapear peticiones de
<http://localhost:3000/welcome/index> a la _acción_ `index` del _controlador_
`welcome`. Esto fue creado al inicio cuando ejecutaste el generador del
_controlador_ (`rails generate controller welcome index`).

Si ingresas a la dirección <http://localhost:3000> en tu navegador, verás el
mensaje `Hello, Rails!` que colocaste dentro de
`app/views/welcome/index.html.erb`, indicando que esta nueva ruta está en
realidad pasando a la _acción_ `index` del _controlador_ `Welcome` y está
renderizando la vista correctamente.

NOTA: Para mayor información acerca del enrutamiento, ir a
[Rails Routing from the Outside In](http://edgeguides.rubyonrails.org/routing.html).

Getting Up and Running
----------------------

Now that you've seen how to create a controller, an action and a view, let's create something with a bit more substance.

In the Blog application, you will now create a new _resource_. A resource is the term used for a collection of similar objects, such as posts, people or animals. You can create, read, update and destroy items for a resource and these operations are referred to as _CRUD_ operations.

In the next section, you will add the ability to create new posts in your application and be able to view them. This is the "C" and the "R" from CRUD: creation and reading. The form for doing this will look like this:

![The new post form](http://edgeguides.rubyonrails.org/images/getting_started/new_post.png)

It will look a little basic for now, but that's ok. We'll look at improving the styling for it afterwards.

### Laying down the ground work

The first thing that you are going to need to create a new post within the application is a place to do that. A great place for that would be at `/posts/new`. If you attempt to navigate to that now -- by visiting [http://localhost:3000/posts/new](http://localhost:3000/posts/new) -- Rails will give you a routing error:

![A routing error, no route matches /posts/new](http://edgeguides.rubyonrails.org/images/getting_started/routing_error_no_route_matches.png)

This is because there is nowhere inside the routes for the application -- defined inside `config/routes.rb` -- that defines this route. By default, Rails has no routes configured at all, besides the root route you defined earlier, and so you must define your routes as you need them.

 To do this, you're going to need to create a route inside `config/routes.rb` file, on a new line between the `do` and the `end` for the `draw` method:

```ruby
get "posts/new"
```

This route is a super-simple route: it defines a new route that only responds to `GET` requests, and that the route is at `posts/new`. But how does it know where to go without the use of the `:to` option? Well, Rails uses a sensible default here: Rails will assume that you want this route to go to the new action inside the posts controller.

With the route defined, requests can now be made to `/posts/new` in the application. Navigate to [http://localhost:3000/posts/new](http://localhost:3000/posts/new) and you'll see another routing error:

![Another routing error, uninitialized constant PostsController](http://edgeguides.rubyonrails.org/images/getting_started/routing_error_no_controller.png)

This error is happening because this route need a controller to be defined. The route is attempting to find that controller so it can serve the request, but with the controller undefined, it just can't do that. The solution to this particular problem is simple: you need to create a controller called `PostsController`. You can do this by running this command:

```bash
$ rails g controller posts
```

If you open up the newly generated `app/controllers/posts_controller.rb` you'll see a fairly empty controller:

```ruby
class PostsController < ApplicationController
end
```

A controller is simply a class that is defined to inherit from `ApplicationController`. It's inside this class that you'll define methods that will become the actions for this controller. These actions will perform CRUD operations on the posts within our system.

If you refresh [http://localhost:3000/posts/new](http://localhost:3000/posts/new) now, you'll get a new error:

![Unknown action new for PostsController!](http://edgeguides.rubyonrails.org/images/getting_started/unknown_action_new_for_posts.png)

This error indicates that Rails cannot find the `new` action inside the `PostsController` that you just generated. This is because when controllers are generated in Rails they are empty by default, unless you tell it you wanted actions during the generation process.

To manually define an action inside a controller, all you need to do is to define a new method inside the controller. Open `app/controllers/posts_controller.rb` and inside the `PostsController` class, define a `new` method like this:

```ruby
def new
end
```

With the `new` method defined in `PostsController`, if you refresh [http://localhost:3000/posts/new](http://localhost:3000/posts/new) you'll see another error:

![Template is missing for posts/new](http://edgeguides.rubyonrails.org/images/getting_started/template_is_missing_posts_new.png)

You're getting this error now because Rails expects plain actions like this one to have views associated with them to display their information. With no view available, Rails errors out.

In the above image, the bottom line has been truncated. Let's see what the full thing looks like:

<blockquote>
Missing template posts/new, application/new with {:locale=>[:en], :formats=>[:html], :handlers=>[:erb, :builder, :coffee]}. Searched in: * "/path/to/blog/app/views"
</blockquote>

That's quite a lot of text! Let's quickly go through and understand what each part of it does.

The first part identifies what template is missing. In this case, it's the `posts/new` template. Rails will first look for this template. If not found, then it will attempt to load a template called `application/new`. It looks for one here because the `PostsController` inherits from `ApplicationController`.

The next part of the message contains a hash. The `:locale` key in this hash simply indicates what spoken language template should be retrieved. By default, this is the English -- or "en" -- template. The next key, `:formats` specifies the format of template to be served in response . The default format is `:html`, and so Rails is looking for an HTML template. The final key, `:handlers`, is telling us what _template handlers_ could be used to render our template. `:erb` is most commonly used for HTML templates, `:builder` is used for XML templates, and `:coffee` uses CoffeeScript to build JavaScript templates.

The final part of this message tells us where Rails has looked for the templates. Templates within a basic Rails application like this are kept in a single location, but in more complex applications it could be many different paths.

The simplest template that would work in this case would be one located at `app/views/posts/new.html.erb`. The extension of this file name is key: the first extension is the _format_ of the template, and the second extension is the _handler_ that will be used. Rails is attempting to find a template called `posts/new` within `app/views` for the application. The format for this template can only be `html` and the handler must be one of `erb`, `builder` or `coffee`. Because you want to create a new HTML form, you will be using the `ERB` language. Therefore the file should be called `posts/new.html.erb` and needs to be located inside the `app/views` directory of the application.

Go ahead now and create a new file at `app/views/posts/new.html.erb` and write this content in it:

```html
<h1>New Post</h1>
```

When you refresh [http://localhost:3000/posts/new](http://localhost:3000/posts/new) you'll now see that the page has a title. The route, controller, action and view are now working harmoniously! It's time to create the form for a new post.

### The first form

To create a form within this template, you will use a <em>form
builder</em>. The primary form builder for Rails is provided by a helper
method called `form_for`. To use this method, add this code into `app/views/posts/new.html.erb`:

```html+erb
<%= form_for :post do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>
```

If you refresh the page now, you'll see the exact same form as in the example. Building forms in Rails is really just that easy!

When you call `form_for`, you pass it an identifying object for this
form. In this case, it's the symbol `:post`. This tells the `form_for`
helper what this form is for. Inside the block for this method, the
`FormBuilder` object -- represented by `f` -- is used to build two labels and two text fields, one each for the title and text of a post. Finally, a call to `submit` on the `f` object will create a submit button for the form.

There's one problem with this form though. If you inspect the HTML that is generated, by viewing the source of the page, you will see that the `action` attribute for the form is pointing at `/posts/new`. This is a problem because this route goes to the very page that you're on right at the moment, and that route should only be used to display the form for a new post.

The form needs to use a different URL in order to go somewhere else.
This can be done quite simply with the `:url` option of `form_for`.
Typically in Rails, the action that is used for new form submissions
like this is called "create", and so the form should be pointed to that action.

Edit the `form_for` line inside `app/views/posts/new.html.erb` to look like this:

```html+erb
<%= form_for :post, :url => { :action => :create } do |f| %>
```

In this example, a `Hash` object is passed to the `:url` option. What Rails will do with this is that it will point the form to the `create` action of the current controller, the `PostsController`, and will send a `POST` request to that route. For this to work, you will need to add a route to `config/routes.rb`, right underneath the one for "posts/new":

```ruby
post "posts" => "posts#create"
```

By using the `post` method rather than the `get` method, Rails will define a route that will only respond to POST methods. The POST method is the typical method used by forms all over the web.

With the form and its associated route defined, you will be able to fill in the form and then click the submit button to begin the process of creating a new post, so go ahead and do that. When you submit the form, you should see a familiar error:

![Unknown action create for PostsController](http://edgeguides.rubyonrails.org/images/getting_started/unknown_action_create_for_posts.png)

You now need to create the `create` action within the `PostsController` for this to work.

### Creating posts

To make the "Unknown action" go away, you can define a `create` action within the `PostsController` class in `app/controllers/posts_controller.rb`, underneath the `new` action:

```ruby
class PostsController < ApplicationController
  def new
  end

  def create
  end

end
```

If you re-submit the form now, you'll see another familiar error: a template is missing. That's ok, we can ignore that for now. What the `create` action should be doing is saving our new post to a database.

When a form is submitted, the fields of the form are sent to Rails as _parameters_. These parameters can then be referenced inside the controller actions, typically to perform a particular task. To see what these parameters look like, change the `create` action to this:

```ruby
def create
  render :text => params[:post].inspect
end
```

The `render` method here is taking a very simple hash with a key of `text` and value of `params[:post].inspect`. The `params` method is the object which represents the parameters (or fields) coming in from the form. The `params` method returns a `HashWithIndifferentAccess` object, which allows you to access the keys of the hash using either strings or symbols. In this situation, the only parameters that matter are the ones from the form.

If you re-submit the form one more time you'll now no longer get the missing template error. Instead, you'll see something that looks like the following:

```ruby
{"title"=>"First post!", "text"=>"This is my first post."}
```

This action is now displaying the parameters for the post that are coming in from the form. However, this isn't really all that helpful. Yes, you can see the parameters but nothing in particular is being done with them.

### Creando el modelo Post

Los Modelos en Rails usan un nombre en singular, y sus correspondientes tablas
de base de datos usan un nombre en plural. Rails provee un generador para crear
modelos, el cual la mayoría de desarrolladores en Rails tienden a usar para
crear nuevos modelos:

```bash
$ rails generate model Post title:string text:text
```

Con ese comando le decimos a Rails que nosotros queremos un modelo `Post`,
junto con un atributo _title_ de tipo _string_, y un atributo _texto_ de tipo
_text_. Esos atributos son automáticamente añadidos a la tabla `posts` en la
base de datos y mapeados al modelo `Post`.

Rails respondió con la creación de un montón de archivos. Por ahora, nosotros
sólo estamos interesados en `app/models/post.rb` y
`db/migrate/20120419084633_create_posts.rb` (en tu caso puede ser un poco
diferente). Este último es responsable de crear la estructura de la base
de datos, que es lo que revisaremos luego.

TIP: Active Record es lo suficientemente inteligente para mapear
automáticamente el nombre de las columnas a atributos del modelo,
lo que significa que tú no tienes que declarar los atributos dentro
de los modelos de Rails, ya que será realizado automáticamente por
Active Record.

### Running a Migration

As we've just seen, `rails generate model` created a _database
migration_ file inside the `db/migrate` directory.
Migrations are Ruby classes that are designed to make it simple to
create and modify database tables. Rails uses rake commands to run migrations,
and it's possible to undo a migration after it's been applied to your database.
Migration filenames include a timestamp to ensure that they're processed in the
order that they were created.

If you look in the `db/migrate/20120419084633_create_posts.rb` file (remember,
yours will have a slightly different name), here's what you'll find:

```ruby
class CreatePosts < ActiveRecord::Migration
  def change
    create_table :posts do |t|
      t.string :title
      t.text :text

      t.timestamps
    end
  end
end
```

The above migration creates a method named `change` which will be called when you
run this migration. The action defined in this method is also reversible, which
means Rails knows how to reverse the change made by this migration, in case you
want to reverse it later. When you run this migration it will create a
`posts` table with one string column and a text column. It also creates two
timestamp fields to allow Rails to track post creation and update times. More
information about Rails migrations can be found in the "Rails Database
Migrations":migrations.html guide.

At this point, you can use a rake command to run the migration:

```bash
$ rake db:migrate
```

Rails will execute this migration command and tell you it created the Posts
table.

```bash
==  CreatePosts: migrating ====================================================
-- create_table(:posts)
   -> 0.0019s
==  CreatePosts: migrated (0.0020s) ===========================================
```

NOTE. Because you're working in the development environment by default, this
command will apply to the database defined in the `development` section of your
`config/database.yml` file. If you would like to execute migrations in another
environment, for instance in production, you must explicitly pass it when
invoking the command: `rake db:migrate RAILS_ENV=production`.

### Saving data in the controller

Back in `posts_controller`, we need to change the `create` action
to use the new `Post` model to save the data in the database. Open that file
and change the `create` action to look like this:

```ruby
def create
  @post = Post.new(params[:post])

  @post.save
  redirect_to :action => :show, :id => @post.id
end
```

Here's what's going on: every Rails model can be initialized with its
respective attributes, which are automatically mapped to the respective
database columns. In the first line we do just that (remember that
`params[:post]` contains the attributes we're interested in). Then,
`@post.save` is responsible for saving the model in the database.
Finally, we redirect the user to the `show` action,
which we'll define later.

TIP: As we'll see later, `@post.save` returns a boolean indicating
wherever the model was saved or not.

### Showing Posts

If you submit the form again now, Rails will complain about not finding
the `show` action. That's not very useful though, so let's add the
`show` action before proceeding. Open `config/routes.rb` and add the following route:

```ruby
get "posts/:id" => "posts#show"
```

The special syntax `:id` tells rails that this route expects an `:id`
parameter, which in our case will be the id of the post. Note that this
time we had to specify the actual mapping, `posts#show` because
otherwise Rails would not know which action to render.

As we did before, we need to add the `show` action in the
`posts_controller` and its respective view.

```ruby
def show
  @post = Post.find(params[:id])
end
```

A couple of things to note. We use `Post.find` to find the post we're
interested in. We also use an instance variable (prefixed by `@`) to
hold a reference to the post object. We do this because Rails will pass all instance
variables to the view.

Now, create a new file `app/view/posts/show.html.erb` with the following
content:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>
```

Finally, if you now go to
[http://localhost:3000/posts/new](http://localhost:3000/posts/new) you'll
be able to create a post. Try it!

![Show action for posts](http://edgeguides.rubyonrails.org/images/getting_started/show_action_for_posts.png)

### Listing all posts

We still need a way to list all our posts, so let's do that. As usual,
we'll need a route placed into `config/routes.rb`:

```ruby
get "posts" => "posts#index"
```

And an action for that route inside the `PostsController` in the `app/controllers/posts_controller.rb` file:

```ruby
def index
  @posts = Post.all
end
```

And then finally a view for this action, located at `app/views/posts/index.html.erb`:

```html+erb
<h1>Listing posts</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>

  <% @posts.each do |post| %>
    <tr>
      <td><%= post.title %></td>
      <td><%= post.text %></td>
    </tr>
  <% end %>
</table>
```

Now if you go to `http://localhost:3000/posts` you will see a list of all the posts that you have created.

### Adding links

You can now create, show, and list posts. Now let's add some links to
navigate through pages.

Open `app/views/welcome/index.html.erb` and modify it as follows:

```html+erb
<h1>Hello, Rails!</h1>
<%= link_to "My Blog", :controller => "posts" %>
```

The `link_to` method is one of Rails' built-in view helpers. It creates a
hyperlink based on text to display and where to go - in this case, to the path
for posts.

Let's add links to the other views as well, starting with adding this "New Post" link to `app/views/posts/index.html.erb`, placing it above the `<!-- <table> -->` tag:

```erb
<%= link_to 'New post', :action => :new %>
```

This link will allow you to bring up the form that lets you create a new post. You should also add a link to this template -- `app/views/posts/new.html.erb` -- to go back to the `index` action. Do this by adding this underneath the form in this template:

```erb
<%= form_for :post do |f| %>
  ...
<% end %>

<%= link_to 'Back', :action => :index %>
```

Finally, add another link to the `app/views/posts/show.html.erb` template to go back to the `index` action as well, so that people who are viewing a single post can go back and view the whole list again:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>

<%= link_to 'Back', :action => :index %>
```

TIP: If you want to link to an action in the same controller, you don't
need to specify the `:controller` option, as Rails will use the current
controller by default.

TIP: In development mode (which is what you're working in by default), Rails
reloads your application with every browser request, so there's no need to stop
and restart the web server when a change is made.

### Permitiendo la actualización de campos

El archivo del modelo `app/models/post.rb` es tan simple como:

```ruby
class Post < ActiveRecord::Base
end
```

No hay mucho en ese archivo - pero noten que la clase `Post` hereda de
`ActiveRecord::Base`. Active Record provee una gran cantidad de funcionalidad a los
modelos de Rails de forma sencilla, incluyendo las operaciones básicas CRUD (del
inglés Create, Read, Update, Destroy) de base de datos, validación de datos así
como el soporte a búsquedas sofisticadas y la habilidad de relacionar múltiples
modelos entre sí.

Rails incluye métodos que ayudaran a asegurar los campos de tu modelo.
Abra el archivo `app/models/post.rb` y complete según se indica:

```ruby
class Post < ActiveRecord::Base
  attr_accessible :text, :title
end
```

Este cambio asegura que todos los cambios realizados a través de formularios HTML
puedan editar los campos `text` y `title`.
No será posible definir la edición de otro campo diferente a través de formularios.
Por supuesto aún será posible definirlo usando el método `field=`.
La accesibilidad de los atributos y el problema de la asignación masiva es cubierto
en detalle en [Security guide](security.html#mass-assignment).

### Agregando algunas validaciones

Rails incluye métodos para ayudarte a validar los datos que son enviados a los modelos.
Abre el archivo `app/models/post.rb` y editalo de la siguiente manera:

```ruby
class Post < ActiveRecord::Base
  attr_accessible :text, :title

  validates :title, :presence => true,
                    :length => { :minimum => 5 }
end
```

Estos cambios asegurarán que todos los artículos tengan un título que sea al menos de cinco caracteres 
de longitud. Rails puede validar una variedad de condiciones en un modelo, incluyendo la presencia o
la unicidad de columnas, sus formatos y la existencia de objetos asociados. Las validaciones están cubiertas
en detalle en [Active Record Validations and Callbacks](active_record_validations_callbacks.html#validations-overview)

Con la validaciones agregadas, cuando llames a `@post.save` en un artículo inválido
retornará `false`. Si abres el archivo `app/controllers/posts_controller.rb`
otra vez, notarás que no verificamos el resultado de la llamada `@post.save`
dentro de la acción `create`. Si `@post.save` falla en esta situación, necesitamos mostrar
el formulario de regreso al usuario. Para hacer esto, cambiar las acciones `new` y `create`
dentro de `app/controllers/posts_controller.rb` a esto:

```ruby
def new
  @post = Post.new
end

def create
  @post = Post.new(params[:post])

  if @post.save
    redirect_to :action => :show, :id => @post.id
  else
    render 'new'
  end
end
```

La acción `new` está ahora creando una nueva instancia llamada `@post`, 
y verás el motivo de ello en un momento.

Notas que dentro de la acción `create` usamos `render`en lugar de `redirect_to` cuando acción `save`
retorna `false`. El método `render`es usado de manera que el objeto `@post`es regresado a la plantilla
`new` cuando es interpretado. Esta interpretación se hace dentro de la misma solicitud que hace el envío
del formulario, mientras que `redirect_to`le dirá al navegador para emitir una nueva solicitud.

Si recargas [http://localhost:3000/posts/new](http://localhost:3000/posts/new) y
tratas de guardar un artículo sin título, Rails enviará de regreso un formulario
pero que no es muy útil. Necesitas decirle al usuario que algo está mal.
Para hacer esto hay que modificar el archivo`app/views/posts/new.html.erb` 
para verificar los mensajes de error:

```html+erb
<%= form_for :post, :url => { :action => :create } do |f| %>
  <% if @post.errors.any? %>
  <div id="errorExplanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
    <% @post.errors.full_messages.each do |msg| %>
      <li><%= msg %></li>
    <% end %>
    </ul>
  </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Back', :action => :index %>
```

Veamos que está pasando. Verificamos si hay errores con
`@post.errors.any?` y en caso que los haya mostramos una lista de todos
los errores con `@post.errors.full_messages`.

`pluralize` es un asistente de Rails que toma un número, un texto y sus argumentos.
Si el número es mayor de 1, el texto será automáticamente pluralizado

La razón de porque agregamos`@post = Post.new` en `posts_controller` es que de otra 
manera `@post` será `nil` en tu vista y llamar a 
`@post.errors.any?` mostrará un error.

CONSEJO: Rails automaticamente ajustará los campos que contienen error en un `div`
dentro de la clase `field_with_errors`. Puedes definir una regla `css`para destacarlos.

Ahora enviarás un bonito mensaje de error cuando intentes guardar un artículo sin título
en [new post form (http://localhost:3000/posts/new)](http://localhost:3000/posts/new).

![Form With Errors](http://edgeguides.rubyonrails.org/images/getting_started/form_with_errors.png)

### Actualizando artículos

Hemos cubierto la parte "CR" del acrónimo CRUD. Ahora nos enfocaremos en la parte "U", actualización
de artículos.

El primer paso será agregar la acción `edit` al `posts_controller`.

Empecemos agregando una ruta a `config/routes.rb`:

```ruby
get "posts/:id/edit" => "posts#edit"
```

Y luego agregar la acción al controlador:

```ruby
def edit
  @post = Post.find(params[:id])
end
```

La vista contendrá un formulario similar al que usamos cuando creamos 
nuevos artículos. Crea un archivo llamado `app/views/posts/edit.html.erb` que contenga 
lo siguiente:

```html+erb
<h1>Editing post</h1>

<%= form_for :post, :url => { :action => :update, :id => @post.id },
:method => :put do |f| %>
  <% if @post.errors.any? %>
  <div id="errorExplanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
    <% @post.errors.full_messages.each do |msg| %>
      <li><%= msg %></li>
    <% end %>
    </ul>
  </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Back', :action => :index %>
```

Esta vez indicamos al formulario la acción `update`, la cual no está definido aún
pero pronto lo estará.

La opción `:method => :put` le dice a Rails que queremos que este formulario sea enviado
a través del método HTTP `PUT`, el cual es el método que tú esperas que se use para
**actualizar** recursos de acuerdo al protocolo REST.

CONSEJO: Por omisión los formularios construidos con el asistente `+form_for_` son enviados 
a través de `POST`.

A continuación, necesitamos agregar la acción `update`. El archivo
`config/routes.rb` necesitará una línea más:

```ruby
put "posts/:id" => "posts#update"
```

Y luego crear la acción `update` en `app/controllers/posts_controller.rb`:

```ruby
def update
  @post = Post.find(params[:id])

  if @post.update_attributes(params[:post])
    redirect_to :action => :show, :id => @post.id
  else
    render 'edit'
  end
end
```

El nuevo método `update_attributes`, es usado cuando deseas acualizar un registro
que ya existe, y acepta un hash conteniendo los atributos que deseas actualizar.
Como hicimos anteriormente, si hay un error actualizando el artículo queremos
mostrar el formulario de regreso al usuario.

CONSEJO: no necesitas enviar todos los atributos a `update_attributes`. Por
ejemplo, si llamas a `@post.update_attributes(:title => 'A new title')`
Rails solo actualizará el atributo `title` sin tocar los otros atributos.

Finalmente, queremos mostrar un enlace a la acción `edit` en la lista de todos
los artículos, de esta manera hacemos que ahora en `app/views/posts/index.html.erb` 
aparezca un nuevo enlace adicional al enlace "Show":

```html+erb
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
    <th></th>
  </tr>

<% @posts.each do |post| %>
  <tr>
    <td><%= post.title %></td>
    <td><%= post.text %></td>
    <td><%= link_to 'Show', :action => :show, :id => post.id %></td>
    <td><%= link_to 'Edit', :action => :edit, :id => post.id %></td>
  </tr>
<% end %>
</table>
```

Y también la agregaremos en la plantilla `app/views/posts/show.html.erb` de manera que 
haya un enlace "Edit" en la página del artículo. Agregar esto al final de tu plantilla: 

```html+erb
...

<%= link_to 'Back', :action => :index %>
| <%= link_to 'Edit', :action => :edit, :id => @post.id %>
```

Y así es como nuestra aplicación se ve hasta el momento

![Index action with edit link](http://edgeguides.rubyonrails.org/images/getting_started/index_action_with_edit_link.png)

### Using partials to clean up duplication in views

`partials` are what Rails uses to remove duplication in views. Here's a
simple example:

```html+erb
# app/views/user/show.html.erb

<h1><%= @user.name %></h1>

<%= render 'user_details' %>

# app/views/user/_user_details.html.erb

<%= @user.location %>

<%= @user.about_me %>
```

The `users/show` template will automatically include the content of the
`users/_user_details` template. Note that partials are prefixed by an underscore,
as to not be confused with regular views. However, you don't include the
underscore when including them with the `helper` method.

TIP: You can read more about partials in the
[Layouts and Rendering in Rails](layouts_and_rendering.html) guide.

Our `edit` action looks very similar to the `new` action, in fact they
both share the same code for displaying the form. Lets clean them up by
using a partial.

Create a new file `app/views/posts/_form.html.erb` with the following
content:

```html+erb
<%= form_for @post do |f| %>
  <% if @post.errors.any? %>
  <div id="errorExplanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
    <% @post.errors.full_messages.each do |msg| %>
      <li><%= msg %></li>
    <% end %>
    </ul>
  </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>
```

Everything except for the `form_for` declaration remained the same.
How `form_for` can figure out the right `action` and `method` attributes
when building the form will be explained in just a moment. For now, let's update the
`app/views/posts/new.html.erb` view to use this new partial, rewriting it
completely:

```html+erb
<h1>New post</h1>

<%= render 'form' %>

<%= link_to 'Back', :action => :index %>
```

Then do the same for the `app/views/posts/edit.html.erb` view:

```html+erb
<h1>Edit post</h1>

<%= render 'form' %>

<%= link_to 'Back', :action => :index %>
```

Point your browser to [http://localhost:3000/posts/new](http://localhost:3000/posts/new) and
try creating a new post. Everything still works. Now try editing the
post and you'll receive the following error:

![Undefined method post_path](http://edgeguides.rubyonrails.org/images/getting_started/undefined_method_post_path.png)

To understand this error, you need to understand how `form_for` works.
When you pass an object to `form_for` and you don't specify a `:url`
option, Rails will try to guess the `action` and `method` options by
checking if the passed object is a new record or not. Rails follows the
REST convention, so to create a new `Post` object it will look for a
route named `posts_path`, and to update a `Post` object it will look for
a route named `post_path` and pass the current object. Similarly, rails
knows that it should create new objects via POST and update them via
PUT.

If you run `rake routes` from the console you'll see that we already
have a `posts_path` route, which was created automatically by Rails when we
defined the route for the index action.
However, we don't have a `post_path` yet, which is the reason why we
received an error before.

```bash
# rake routes

    posts GET  /posts(.:format)            posts#index
posts_new GET  /posts/new(.:format)        posts#new
          POST /posts(.:format)            posts#create
          GET  /posts/:id(.:format)        posts#show
          GET  /posts/:id/edit(.:format)   posts#edit
          PUT  /posts/:id(.:format)        posts#update
     root      /                           welcome#index
```

To fix this, open `config/routes.rb` and modify the `get "posts/:id"`
line like this:

```ruby
get "posts/:id" => "posts#show", :as => :post
```

The `:as` option tells the `get` method that we want to make routing helpers
called `post_url` and `post_path` available to our application. These are
precisely the methods that the `form_for` needs when editing a post, and so now
you'll be able to update posts again.

NOTE: The `:as` option is available on the `post`, `put`, `delete` and `match`
routing methods also.

### Eliminando artículos

Ahora estamos listos para cubrir la parte "D" del acrónimo CRUD: eliminar artículos
en la base de datos. Siguiendo la convención REST, vamos a agregar una ruta para la
eliminación de artículos a `config/routes.rb`:

```ruby
delete "posts/:id" => "posts#destroy"
```
El método de enrutamiento `delete` debe ser usado para métodos que destruyen recursos.
Si se deja como un típico comando de ruteo `get`, es posible que se puedan enviar
URLs malintencionadas como estas:

```html
<a href='http://yoursite.com/posts/1/destroy'>look at this cat!</a>
```

Nosotros usamos el método `delete` para destruir recursos y este ruteo está enlazado
con la acción `destroy` dentro de `app/controllers/posts_controller.rb`, la cual no existe
aún pero que se muestra a continuación:

```ruby
def destroy
  @post = Post.find(params[:id])
  @post.destroy

  redirect_to :action => :index
end
```

Puedes llamar a `destroy` en objetos Active Record cuando desees eliminarlos de la
base de datos. Hay que tener en cuenta que no necesitas agregar una vista para esta acción ya que
estamos siendo redireccionados a la acción `index`.

Finalmente, agregamos un enlace a la plantilla de la acción `index`
(`app/views/posts/index.html.erb`) para completar todo.

```html+erb
<h1>Listing Posts</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
    <th></th>
    <th></th>
  </tr>

<% @posts.each do |post| %>
  <tr>
    <td><%= post.title %></td>
    <td><%= post.text %></td>
    <td><%= link_to 'Show', :action => :show, :id => post.id %></td>
    <td><%= link_to 'Edit', :action => :edit, :id => post.id %></td>
    <td><%= link_to 'Destroy', { :action => :destroy, :id => post.id }, :method => :delete, :data => { :confirm => 'Are you sure?' } %></td>
  </tr>
<% end %>
</table>
```
Usaremos aquí `link_to` de diferente manera. Empaquetaremos los atributos
`:action` y `:id` en un hash de manera que podamos pasar las dos claves como uno
en un solo argumento y finalmente las otras dos claves como otro argumento.
Las opciones `:method` y `:'data-confirm'` son usadas como atributos HTML de manera de que cuando
se hace clic en el enlace Rails mostrará un diálogo de confirmación al usuario
y luego direccionará al enlace con el método `delete`.
Esto es realizado a través de un archivo JavaScript `jquery_ujs` el cual fue automáticamente
incluido dentro del diseño de tu aplicación (`app/views/layouts/application.html.erb`) cuando
la aplicación fue generada. Sin este archivo el diálogo de confirmación no aparecerá.

![Confirm Dialog](http://edgeguides.rubyonrails.org/images/getting_started/confirm_dialog.png)

Felicitaciones, ahora puedes crear, mostrar, enumerar, actualizar y eliminar
artículos. En la siguiente sección veremos cómo Rails puede ayudarnos en la creación de
aplicaciones REST, y cómo podemos refactorizar nuestro Blog  para tomar
ventaja de ello.

### Profundizando en REST

Ya hemos cubierto todas las acciones CRUD de una aplicación REST.
Lo hicimos declarando rutas separadas con los verbos adecuados en
`config/routes.rb`. Así es como se ve el archivo hasta ahora:

```ruby
get "posts" => "posts#index"
get "posts/new"
post "posts" => "posts#create"
get "posts/:id" => "posts#show", :as => :post
get "posts/:id/edit" => "posts#edit"
put "posts/:id" => "posts#update"
delete "posts/:id" => "posts#destroy"
```

Eso es un montón de código para cubrir un único **recurso**. Afortunadamente,
Rails proporciona un método llamado `resources` el cual puede ser usado para
declarar un recurso REST estándar. Así es como el archivo `config/routes.rb`
se ve luego de utilizar `resources`:

```ruby
Blog::Application.routes.draw do

  resources :posts

  root :to => "welcome#index"
end
```

Si ejecutas `rake routes`, podrás ver que todas las rutas que
declaramos anteriormente aún están disponibles:

```bash
# rake routes
    posts GET    /posts(.:format)          posts#index
          POST   /posts(.:format)          posts#create
 new_post GET    /posts/new(.:format)      posts#new
edit_post GET    /posts/:id/edit(.:format) posts#edit
     post GET    /posts/:id(.:format)      posts#show
          PUT    /posts/:id(.:format)      posts#update
          DELETE /posts/:id(.:format)      posts#destroy
     root        /                         welcome#index
```

Además, si vas a través de las acciones de creación, actualización
y eliminación de posts, la aplicación sigue funcionando como antes.

TIP: En general, Rails fomenta el uso de recursos (`resources`) en lugar
de declarar las rutas manualmente. Se hizo solamente en esta guía como
un ejercicio de aprendizaje. Para más información acerca de _routing_,
mira [Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html).

Agregando un Segundo Modelo
---------------------------

Es hora de agregar un segundo modelo a la aplicación. El segundo modelo debe
manejar los comentarios de los artículos.

### Generando un Modelo

Vamos a usar el mismo generador que usamos antes al crear el modelo `Post`. Esta
vez crearemos el modelo `Comment` para los comentarios del artículo. Ejecuta
esto en tu terminal:

```bash
$ rails generate model Comment commenter:string body:text post:references
```

Este comando generará cuatro archivos:

| Archivo                                      | Propósito                                                                                                |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------|
| db/migrate/20100207235629_create_comments.rb | Migración para crear la tabla de comentarios en tu base de datos (en tu caso con un timestamp diferente).|
| app/models/comment.rb                        | El modelo Comment.                                                                                       |
| test/unit/comment_test.rb                    | Prubas unitarias para el modelo de comentarios.                                                          |
| test/fixtures/comments.yml                   | Muestras de comentarios para usar de pruebas.                                                            |

Primero, miremos `comment.rb`:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :post
  attr_accessible :body, :commenter
end
```

Ésto es muy similar al modelo `post.rb` que vimos antes. La diferencia es la
línea `belongs_to :post`, que establece una asociación de Active Record.
Vas a aprender un poco más sobre asociaciones en la siguiente sección de esta
guía.

Además del modelo, Rails hizo la migración para crear la tabla correspondiente
en la base de datos:

```ruby
class CreateComments < ActiveRecord::Migration
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :post

      t.timestamps
    end

    add_index :comments, :post_id
  end
end
```

La línea `t.references` establece una columna _foreign key_ para la asociación
entre los dos modelos. La línea `add_index` establece un index para esta columna
de la asociación. Corre la migración:

```bash
$ rake db:migrate
```

Rails es suficientemente listo para sólo ejecutar las migraciones que no se han
ejecutado todavía en la base de datos actual, así que en este caso sólo verás:

```bash
==  CreateComments: migrating =================================================
-- create_table(:comments)
   -> 0.0008s
-- add_index(:comments, :post_id)
   -> 0.0003s
==  CreateComments: migrated (0.0012s) ========================================
```

### Asociando Modelos

Las asociaciones de Active Record te permiten declarar fácilmente la relación
entre dos modelos. En el caso de los comentarios y artículos, puedes escribir la
relación de esta manera:

* Cada comentario pertence a un artículo.
* Un artículo puede tener muchos comentarios.

De hecho, ésto es muy cercano a la sintáxis que usa Rails para declarar esta
asociación. Ya has visto la línea de código en el modelo `Comment` que hace que
cada comentario pertenezca a un artículo:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :post
end
```

Vas a tener que editar el archivo `post.rb` para agregar el otro lado de la
asociación:

```ruby
class Post < ActiveRecord::Base
  validates :title, :presence => true,
                    :length => { :minimum => 5 }

  has_many :comments
end
```

Estas dos declaraciones permiten bastante comportamiento automatizado. Por
ejemplo, si tienes una variable de instancia `@post` conteniendo un artículo,
puedes obtener todos los comentarios que pertenecen a ese artículo como un
arreglo usando `@post.comments`.

SUGERENCIA: Para más información sobre las asociaciones de Active Record, revisa
la guía [Active Record Associations](http://guides.rubyonrails.org/association_basics.html)
(en inglés).

### Agregando una Ruta para Comentarios

Así como con el controlador `welcome`, vamos a necesitar agregar una ruta para
que Rails sepa donde queremos navegar para ver `comments`. Abre el archivo
`config/routes.rb` nuevamente, y edítalo de la siguiente manera:

```ruby
resources :posts do
  resources :comments
end
```

Ésto crea `comments` como un _recurso anidado_ dentro de `posts`. Esta es otra
parte de capturar la relación jerárquica que existe entre artículos y
comentarios.

SUGERENCIA: Para más información sobre el ruteo, mira la guía
[Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html)
(en inglés).

### Generando un Controlador

Con el modelo terminado, necesitamos crearle un controlador. Nuevamente,
usaremos el mismo generador que antes:

```bash
$ rails generate controller Comments
```

Esto crea seis diferentes archivos y una carpeta vacía:

| Archivo/Carpeta                             | Propósito                                   |
| ------------------------------------------- | --------------------------------------------|
| app/controllers/comments_controller.rb      | El controlador de Comments.                 |
| app/views/comments/                         | Donde se guardan las vistas del controlador.|
| test/functional/comments_controller_test.rb | Las pruebas funcionales del controlador.    |
| app/helpers/comments_helper.rb              | El helper de la vista.                      |
| test/unit/helpers/comments_helper_test.rb   | Las pruebas unitarias para el helper.       |
| app/assets/javascripts/comment.js.coffee    | CoffeeScript para el controlador.           |
| app/assets/stylesheets/comment.css.scss     | Hojas de estilo para el controlador.        |

Como con cualquier blog, nuestros lectores crearán sus comentarios directamente
después de leer el artículo, y una vez que agregaron su comentario, serán
enviados de vuelta al artículo para ver su comentario ahora listado. Debido a
esto, nuestro `CommentsController` está ahí para proveer un método para crear
comentarios y eliminar spam cuando aparezca.

Así que primero, vamos a armar la plantilla `show` del artículo
(`/app/views/posts/show.html.erb`) para que nos permita hacer comentarios:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>

<h2>Add a comment:</h2>
<%= form_for([@post, @post.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br />
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br />
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit Post', edit_post_path(@post) %> |
<%= link_to 'Back to Posts', posts_path %>
```

Ésto agrega un formulario en la vista `show` del artítculo que crea un
comentario al llamar a la acción `create` en el `CommentsController`. Al llamar
`form_for` se necesita pasar un arreglo, que construirá una ruta anidada,
siguiendo el esquema `/posts/1/comments`.

Armemos la acción `create`:

```ruby
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(params[:comment])
    redirect_to post_path(@post)
  end
end
```

Verás un poco más de complejidad aquí comparado a lo visto en el controlador de
artículos. Eso es un efecto secundario del anidado que estás usando. Cada vez
que se crea un comentario es necesario saber a que artículo pertenece. Por eso
la primera llamada al método `find` del modelo `Post`, para ubicar el artículo
en particular.

Además, el código trata de tomar ventaja de algunos de los métodos disponibles
a las asociaciones. Usamos el método `create` en `@post.comments` para crear y
guardar el comentario. Esto asociará automaticamente el comentario el artículo
en particular.

Una vez que hemos hecho el comentario nuevo, enviamos al usuario de vuelta al
artículo original usando el helper `post_path(@post)`. Como hemos podido ver,
ésto luego llama a la acción `show` en el `PostsController` que hace render con
la plantilla `show.html.erb`. Aquí es donde queremos mostrar los comentarios,
así que agreguemos `app/views/posts/show.html.erb`.

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>

<h2>Comments</h2>
<% @post.comments.each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>

  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>

<h2>Add a comment:</h2>
<%= form_for([@post, @post.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br />
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br />
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit Post', edit_post_path(@post) %> |
<%= link_to 'Back to Posts', posts_path %>
```

Ahora puedes agregar artículos y comentarios a tu blog, y hacer que se muestren
en los lugares correoctos.

![Artículo con Comentarios](http://edgeguides.rubyonrails.org/images/getting_started/post_with_comments.png)

Haciendo Refactoring
--------------------

Ahora que tenemos los artículos y comentarios funcionando, dale una mirada a la
plantilla `app/views/posts/show.html.erb`. Se está volviendo larga y complicada.
Podemos usar parciales (_partials_) para simplificarla.

### Haciendo Render de Colecciones de Parciales

Primero, creemos el parcial de comentario para extraer el mostrar de todos los
comentarios del artículo. Crea el archivo `app/views/comments/_comment.html.erb`
y coloca lo siguiente:

```html+erb
<p>
  <strong>Commenter:</strong>
  <%= comment.commenter %>
</p>

<p>
  <strong>Comment:</strong>
  <%= comment.body %>
</p>
```

Luego puedes cambiar `app/views/posts/show.html.erb` para que se vea de esta
manera:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>

<h2>Comments</h2>
<%= render @post.comments %>

<h2>Add a comment:</h2>
<%= form_for([@post, @post.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br />
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br />
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit Post', edit_post_path(@post) %> |
<%= link_to 'Back to Posts', posts_path %>
```

Ésto hará que el parcial en `app/views/comments/_comment.html.erb` se haga
render una vez por cada comentario en la colección `@post.comments`. A medida
que el método `render` itera sobre la coleción `@post.comments`, asigna cada
comentario a la variable local llamada igual que el parcial, en este caso
`comment` que luego está disponible en el parcial para que la usemos.

### Haciendo Render de un Parcial de Formulario

Movamos también la sección de comentarios nuevos a su propio parcial. De nuevo,
crea un archivo `app/views/comments/_form.html.erb` que contenga:

```html+erb
<%= form_for([@post, @post.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br />
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br />
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

Luego haz que `app/views/posts/show.html.erb` se vea de la siguiente manera:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>

<h2>Add a comment:</h2>
<%= render "comments/form" %>

<%= link_to 'Edit Post', edit_post_path(@post) %> |
<%= link_to 'Back to Posts', posts_path %>
```

El segundo render sólo define la plantilla parcial que queremos usar,
`comments/form`. Rails es suficientemente inteligente para detectar el slash en
el texto y darse cuenta que lo que quieres es hacer render del archivo
`_form.html.erb` en la carpeta `app/views/comments`.

El objeto `@post` está disponible a cualquier parcial al que se le haga render
en la vista porque lo hemos definido como una variable de instancia.

Eliminando Comentarios
----------------------

Otra funcionalidad importante para un blog es poder eliminar comentarios spam.
Para hacer esto, necesitamos implementar un enlace de algún tipo en la vista, y
una acción `DELETE` en el `CommentsController`.

Primero, agreguemos el enlace para eliminar en el parcial
`app/views/comments/_comment.html.erb`:

```html+erb
<p>
  <strong>Commenter:</strong>
  <%= comment.commenter %>
</p>

<p>
  <strong>Comment:</strong>
  <%= comment.body %>
</p>

<p>
  <%= link_to 'Eliminar Comentario', [comment.post, comment],
               :method => :delete,
               :data => { :confirm => '¿Estás seguro?' } %>
</p>
```

Al hacer click en este nuevo enlace "Eliminar Comentario" se enviará un `DELETE
/posts/:id/comments/:id` a nuestro `CommentsController`, que puede luego usar
para ubicar el comentario que queremos eliminar, así que agreguemos una acción
de eliminar a nuestro controlador:

```ruby
class CommentsController < ApplicationController

  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(params[:comment])
    redirect_to post_path(@post)
  end

  def destroy
    @post = Post.find(params[:post_id])
    @comment = @post.comments.find(params[:id])
    @comment.destroy
    redirect_to post_path(@post)
  end

end
```

La acción `destroy` encontrará el artículo que estamos viendo, luego el
comentario en la colección `@post.comments`, para eliminarlo de la base de datos
y enviarnos de vuelta a la acción `show` para el artículo.


### Eliminando Objetos Asociados

Si eliminas un artículo entonces sus comentarios asociados necesitas ser
eliminados también. Si no lo haces simplemente van a ocupar espacio en la base
de datos. Rails te permite usar la opción `dependent` en las asociaciones para
lograrlo. Modifica el modelo Post, en `app/models/post.rb`, de esta manera:

```ruby
class Post < ActiveRecord::Base
  validates :title, :presence => true,
                    :length => { :minimum => 5 }
  has_many :comments, :dependent => :destroy
end
```

Seguridad
---------

Si fueras a publicar tu blog en línea, cualquier persona podría agregar, editar
y eliminar artículos o eliminar comentarios.

Rails provee un sistema muy simple de autenticación por HTTP que funcionaría muy
bien en esta situación.

Necesitamos una forma de bloquear el acceso a ciertas acciones en el controlador
`PostsController` si la persona no está autenticada, aquí podemos usar el método
de Rails `http_basic_authenticate_with`, que permite acceso a la acción
solicitada si el método retorna `true`.

Para usar el sistema de autenticación, lo especificamos en la parte inicial de
`PostsController`, en este caso, queremos autenticar al usuario en cada una de
las acciones, excepto `index` y `show`, así lo escribimos:

```ruby
class PostsController < ApplicationController

  http_basic_authenticate_with :name => "dhh", :password => "secret", :except => [:index, :show]

  def index
    @posts = Post.all
# cortado por brevedad
```

También queremos limitar la eliminación de comentarios a los usuarios autenticados, así
que en `CommentsController` escribimos:

```ruby
class CommentsController < ApplicationController

  http_basic_authenticate_with :name => "dhh", :password => "secret", :only => :destroy

  def create
    @post = Post.find(params[:post_id])
# cortado por brevedad
```

Ahora si intentamos crear un nuevo artículo, vas a ser recibido con una ventana
de diálogo de autenticación HTTP básica.

![Ventana de diálogo de autenticación HTTP básica](http://edgeguides.rubyonrails.org/images/challenge.png)

¿Qué sigue?
-----------

Ahora que has visto tu primera aplicación en Rails, deberías sentir la libertad
de actualizarla y experimentar por tu cuenta. Pero no necesitas hacer todo sin
ayuda. A medida que vayas necesitando ayuda mientras comienzas con Rails, puedes
consultar estos recursos:

**Inglés**

* Las [guías de Ruby on Rails](http://guides.rubyonrails.org).
* El [tutorial de Ruby on Rails](http://railstutorial.org/book).
* La [lista de correo de Ruby on Rails](http://groups.google.com/group/rubyonrails-talk).
* El canal en irc.freenode.net [#rubyonrails](irc://irc.freenode.net/#rubyonrails).

**Español**

* El grupo [Ruby Perú](http://ruby.pe).
* El grupo [Ruby Sur](http://rubysur.org).

Rails viene con ayuda incorporada que puedes generar usando `rake` en la línea
de comando:

* Ejecuta `rake doc:guides` para generar una copia completa de las guías de
Rails (en inglés) en la carpeta `doc/guides` dentro de tu aplicación. Abre
`doc/guides/index.html` en tu navegador para explorar las guías.
* Ejecuta `rake doc:rails` genera una copia completa de la documentación del API
de Rails en la carpeta `doc/api` de tu aplicación. Abre `doc/api/index.html` en
tu navegador para explorar la documentación del API.

Errores Comunes de Configuración
--------------------------------

La forma más fácil de trabajar con Rails es guardando toda los datos externos
como UTF-8. Si no lo haces, por lo general las librerías de Ruby y Rails van a
ser capaces de convertir tus datos nativos a UTF-8, pero esto no funciona en
todos los casos, así que lo ideal es asegurarte que todos tus datos externos
usen UTF-8.

Si has cometido un error de este tipo, el síntoma más común es un símbolo de un
diamante negro con un signo de interrogación en vez de algunos caracteres en tu
navegador. Otro síntoma común es ver caracteres como "Ã¼" apareciendo en vez de
la "ü" por ejemplo. Rails realiza una serie de pasos internos para resolver
casos comunes. Sin embargo, si tienes datos externos que no están guardados en
UTF-8, puede resultar en este tipo de problemas al no ser automáticamente
detectados y resueltos por Rails.

Dos fuentes comunes de datos que no están en UTF-8:

* Tu editor de texto: La mayoría de editores de texto (como TextMate, o Sublime
  Text), guardan los archivos en UTF-8 por defecto. Si tu editor no lo hace,
  esto puede resultar en los problemas mencionados arriba. Esto también aplica
  a los archivos de traducción para I18n. La mayoría de editores que no usan
  UTF-8 por defecto (como algunas versionesde Dreamweaver) ofrecen una manera
  para cambiar la opción por defecto a UTF-8. Házlo!
* Tu base de datos. Rails convierte los datos que intercambia con tu base de
  datos a UTF-8 por defecto. Sin embargo, si tu base de datos no está usando
  UTF-8 internamente, puede no ser capaz de guardar todos los datos que ingresen
  tus usuarios. Por ejemplo, si tu base de datos está usando Latin-1
  internamente, y tus usuarios ingresan caracteres rusos, hebreos o japoneses,
  esos datos serán perdidos para siempre una vez que entren a la base de datos.
  Si es posible, usa UTF-8 internamente para el almacenamiento de datos.
