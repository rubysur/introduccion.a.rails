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
-------------

Rails es un framework de desarrollo de aplicaciones web escrito en el
lenguaje de programación Ruby. Está diseñado para hacer que la programación
de aplicaciones web sea más fácil, haciendo supuestos sobre lo que cada
desarrollador necesita para comenzar. It allows you to write less code while
accomplishing more than many other languages and frameworks. Además, expertos
desarrolladores en Rails reportan que hace que el desarrollo de aplicaciones
web sea más divertido.

Rails es un software dogmático. Éste asume que existe una forma "mejor" de hacer
las cosas, y esta diseñado para formentar esa forma - y en algunos casos para
desalentar alternativas. Si aprendes "El Modo Rails" probablemente descubrirás
un tremendo incremento en productividad. Si persistes trayendo viejos hábitos
de otros lenguajes a tu desarrollo Rails, e intentas usar patrones aprendidos en
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
al ingresar a la raíz de nuestro sitio, [http://localhost:3000](http://localhost:3000).
Por el momento, sin embargo, la página "Welcome Aboard" está ocupando ese lugar.

Para arreglarlo, borramos el archivo `index.html` ubicado dentro de la carpeta
`public` de la aplicación.

Necesitas hacer esto debido a que Rails servirá cualquier archivo estático en la
carpeta `public` que coincida con una ruta, en preferencia a cualquier contenido
que puedas generar desde los _controladores_. El archivo `index.html` es
especial: éste será servido si una petición llega a la ruta raíz, por ejemplo
http://localhost:3000. Si otra petición tal como http://localhost:3000/welcome
ocurriera, un archivo estático en `public/welcome.html` sería servido primero,
pero sólo si existiera.

A continuación, tienes que indicarle a Rails donde tu página principal esta
ubicada.

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
peticiones entrantes a _controladores_ y _acciones_. Este archivo contiene muchos
rutas de ejemplo en líneas comentadas, y una de ellas en realidad muestra como
conectar la raíz de tu sitio a un _controlador_ y _acción_ específico. Encuentra
la línea iniciando con `root :to` y descoméntala. Debería verse como lo siguiente:

```ruby
root :to => "welcome#index"
```

El `root :to => "welcome#index"` le indica a Rails mapear peticiones de la raíz
de la aplicación a la _acción_ `index` del _controlador_ `welcome` y
`get "welcome/index"` le indica a Rails mapear peticiones de
[http://localhost:3000/welcome/index](http://localhost:3000/welcome/index)
a la _acción_ `index` del _controlador_ `welcome`. Esto fue creado al inicio cuando
ejecutaste el generador del _controlador_
(`rails generate controller welcome index`).

Si ingresas a la dirección [http://localhost:3000](http://localhost:3000) en tu
navegador, verás el mensaje `Hello, Rails!` que colocaste dentro de
`app/views/welcome/index.html.erb`, indicando que esta nueva ruta esta en
realidad pasando a la _acción_ `index` del _controlador_ `Welcome` y esta
renderizando la vista correctamente.

NOTA: Para mayor información acerca del enrutamiento, ir a
[Enrutamiento en Rails de Afuera hacia dentro](http://edgeguides.rubyonrails.org/routing.html).

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

Let's add links to the other views as well, starting with adding this "New Post" link to `app/views/posts/index.html.erb`, placing it above the `<table>` tag:

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

### Adding Some Validation

Rails includes methods to help you validate the data that you send to models.
Open the `app/models/post.rb` file and edit it:

```ruby
class Post < ActiveRecord::Base
  attr_accessible :text, :title

  validates :title, :presence => true,
                    :length => { :minimum => 5 }
end
```

These changes will ensure that all posts have a title that is at least five characters long.
Rails can validate a variety of conditions in a model, including the presence or uniqueness of columns, their
format, and the existence of associated objects. Validations are covered in detail
in [Active Record Validations and Callbacks](active_record_validations_callbacks.html#validations-overview)

With the validation now in place, when you call `@post.save` on an invalid
post, it will return `false`. If you open `app/controllers/posts_controller.rb`
again, you'll notice that we don't check the result of calling `@post.save`
inside the `create` action. If `@post.save` fails in this situation, we need to
show the form back to the user. To do this, change the `new` and `create`
actions inside `app/controllers/posts_controller.rb` to these:

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

The `new` action is now creating a new instance variable called `@post`, and
you'll see why that is in just a few moments.

Notice that inside the `create` action we use `render` instead of `redirect_to` when `save`
returns `false`. The `render` method is used so that the `@post` object is passed back to the `new` template when it is rendered. This rendering is done within the same request as the form submission, whereas the `redirect_to` will tell the browser to issue another request.

If you reload
[http://localhost:3000/posts/new](http://localhost:3000/posts/new) and
try to save a post without a title, Rails will send you back to the
form, but that's not very useful. You need to tell the user that
something went wrong. To do that, you'll modify
`app/views/posts/new.html.erb` to check for error messages:

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

A few things are going on. We check if there are any errors with
`@post.errors.any?`, and in that case we show a list of all
errors with `@post.errors.full_messages`.

`pluralize` is a rails helper that takes a number and a string as its
arguments. If the number is greater than one, the string will be automatically pluralized.

The reason why we added `@post = Post.new` in `posts_controller` is that
otherwise `@post` would be `nil` in our view, and calling
`@post.errors.any?` would throw an error.

TIP: Rails automatically wraps fields that contain an error with a div
with class `field_with_errors`. You can define a css rule to make them
standout.

Now you'll get a nice error message when saving a post without title when you
attempt to do just that on the [new post form (http://localhost:3000/posts/new)](http://localhost:3000/posts/new).

![Form With Errors](http://edgeguides.rubyonrails.org/images/getting_started/form_with_errors.png)

### Updating Posts

We've covered the "CR" part of CRUD. Now let's focus on the "U" part,
updating posts.

The first step we'll take is adding a `edit` action to
`posts_controller`.

Start by adding a route to `config/routes.rb`:

```ruby
get "posts/:id/edit" => "posts#edit"
```

And then add the controller action:

```ruby
def edit
  @post = Post.find(params[:id])
end
```

The view will contain a form similar to the one we used when creating
new posts. Create a file called `app/views/posts/edit.html.erb` and make
it look as follows:

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

This time we point the form to the `update` action, which is not defined yet
but will be very soon.

The `:method => :put` option tells Rails that we want this form to be
submitted via the `PUT`, HTTP method which is the HTTP method you're expected to use to
**update** resources according to the REST protocol.

TIP: By default forms built with the +form_for_ helper are sent via `POST`.

Next, we need to add the `update` action. The file
`config/routes.rb` will need just one more line:

```ruby
put "posts/:id" => "posts#update"
```

And then create the `update` action in `app/controllers/posts_controller.rb`:

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

The new method, `update_attributes`, is used when you want to update a record
that already exists, and it accepts a hash containing the attributes
that you want to update. As before, if there was an error updating the
post we want to show the form back to the user.

TIP: you don't need to pass all attributes to `update_attributes`. For
example, if you'd call `@post.update_attributes(:title => 'A new title')`
Rails would only update the `title` attribute, leaving all other
attributes untouched.

Finally, we want to show a link to the `edit` action in the list of all the
posts, so let's add that now to `app/views/posts/index.html.erb` to make it
appear next to the "Show" link:

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

And we'll also add one to the `app/views/posts/show.html.erb` template as well,
so that there's also an "Edit" link on a post's page. Add this at the bottom of
the template:

```html+erb
...

<%= link_to 'Back', :action => :index %>
| <%= link_to 'Edit', :action => :edit, :id => @post.id %>
```

And here's how our app looks so far:

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

### Deleting Posts

We're now ready to cover the "D" part of CRUD, deleting posts from the
database. Following the REST convention, we're going to add a route for
deleting posts to `config/routes.rb`:

```ruby
delete "posts/:id" => "posts#destroy"
```

The `delete` routing method should be used for routes that destroy
resources. If this was left as a typical `get` route, it could be possible for
people to craft malicious URLs like this:

```html
<a href='http://yoursite.com/posts/1/destroy'>look at this cat!</a>
```

We use the `delete` method for destroying resources, and this route is mapped to
the `destroy` action inside `app/controllers/posts_controller.rb`, which doesn't exist yet, but is
provided below:

```ruby
def destroy
  @post = Post.find(params[:id])
  @post.destroy

  redirect_to :action => :index
end
```

You can call `destroy` on Active Record objects when you want to delete
them from the database. Note that we don't need to add a view for this
action since we're redirecting to the `index` action.

Finally, add a 'destroy' link to your `index` action template
(`app/views/posts/index.html.erb`) to wrap everything
together.

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

Here we're using `link_to` in a different way. We wrap the
`:action` and `:id` attributes in a hash so that we can pass those two keys in
first as one argument, and then the final two keys as another argument. The `:method` and `:'data-confirm'`
options are used as HTML5 attributes so that when the link is clicked,
Rails will first show a confirm dialog to the user, and then submit the link with method `delete`.
This is done via the JavaScript file `jquery_ujs` which is automatically included
into your application's layout (`app/views/layouts/application.html.erb`) when you
generated the application. Without this file, the confirmation dialog box wouldn't appear.

![Confirm Dialog](http://edgeguides.rubyonrails.org/images/getting_started/confirm_dialog.png)

Congratulations, you can now create, show, list, update and destroy
posts. In the next section will see how Rails can aid us when creating
REST applications, and how we can refactor our Blog app to take
advantage of it.

### Going Deeper into REST

We've now covered all the CRUD actions of a REST app. We did so by
declaring separate routes with the appropriate verbs into
`config/routes.rb`. Here's how that file looks so far:

```ruby
get "posts" => "posts#index"
get "posts/new"
post "posts" => "posts#create"
get "posts/:id" => "posts#show", :as => :post
get "posts/:id/edit" => "posts#edit"
put "posts/:id" => "posts#update"
delete "posts/:id" => "posts#destroy"
```

That's a lot to type for covering a single **resource**. Fortunately,
Rails provides a `resources` method which can be used to declare a
standard REST resource. Here's how `config/routes.rb` looks after the
cleanup:

```ruby
Blog::Application.routes.draw do

  resources :posts

  root :to => "welcome#index"
end
```

If you run `rake routes`, you'll see that all the routes that we
declared before are still available:

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

Also, if you go through the motions of creating, updating and deleting
posts the app still works as before.

TIP: In general, Rails encourages the use of resources objects in place
of declaring routes manually. It was only done in this guide as a learning
exercise. For more information about routing, see
[Rails Routing from the Outside In](routing.html).

Adding a Second Model
---------------------

It's time to add a second model to the application. The second model will handle comments on
posts.

### Generating a Model

We're going to see the same generator that we used before when creating
the `Post` model. This time we'll create a `Comment` model to hold
reference of post comments. Run this command in your terminal:

```bash
$ rails generate model Comment commenter:string body:text post:references
```

This command will generate four files:

| File                                         | Purpose                                                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| db/migrate/20100207235629_create_comments.rb | Migration to create the comments table in your database (your name will include a different timestamp) |
| app/models/comment.rb                        | The Comment model                                                                                      |
| test/unit/comment_test.rb                    | Unit testing harness for the comments model                                                            |
| test/fixtures/comments.yml                   | Sample comments for use in testing                                                                     |

First, take a look at `comment.rb`:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :post
  attr_accessible :body, :commenter
end
```

This is very similar to the `post.rb` model that you saw earlier. The difference
is the line `belongs_to :post`, which sets up an Active Record _association_.
You'll learn a little about associations in the next section of this guide.

In addition to the model, Rails has also made a migration to create the
corresponding database table:

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

The `t.references` line sets up a foreign key column for the association between
the two models. And the `add_index` line sets up an index for this association
column. Go ahead and run the migration:

```bash
$ rake db:migrate
```

Rails is smart enough to only execute the migrations that have not already been
run against the current database, so in this case you will just see:

```bash
==  CreateComments: migrating =================================================
-- create_table(:comments)
   -> 0.0008s
-- add_index(:comments, :post_id)
   -> 0.0003s
==  CreateComments: migrated (0.0012s) ========================================
```

### Associating Models

Active Record associations let you easily declare the relationship between two
models. In the case of comments and posts, you could write out the relationships
this way:

* Each comment belongs to one post.
* One post can have many comments.

In fact, this is very close to the syntax that Rails uses to declare this
association. You've already seen the line of code inside the Comment model that
makes each comment belong to a Post:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :post
end
```

You'll need to edit the `post.rb` file to add the other side of the association:

```ruby
class Post < ActiveRecord::Base
  validates :title, :presence => true,
                    :length => { :minimum => 5 }

  has_many :comments
end
```

These two declarations enable a good bit of automatic behavior. For example, if
you have an instance variable `@post` containing a post, you can retrieve all
the comments belonging to that post as an array using `@post.comments`.

TIP: For more information on Active Record associations, see the "Active Record
Associations":association_basics.html guide.

### Adding a Route for Comments

As with the `welcome` controller, we will need to add a route so that Rails knows
where we would like to navigate to see `comments`. Open up the
`config/routes.rb` file again, and edit it as follows:

```ruby
resources :posts do
  resources :comments
end
```

This creates `comments` as a _nested resource_ within `posts`. This is another
part of capturing the hierarchical relationship that exists between posts and
comments.

TIP: For more information on routing, see the "Rails Routing from the Outside
In":routing.html guide.

### Generating a Controller

With the model in hand, you can turn your attention to creating a matching
controller. Again, we'll use the same generator we used before:

```bash
$ rails generate controller Comments
```

This creates six files and one empty directory:

| File/Directory                              | Purpose                                  |
| ------------------------------------------- | ---------------------------------------- |
| app/controllers/comments_controller.rb      | The Comments controller                  |
| app/views/comments/                         | Views of the controller are stored here  |
| test/functional/comments_controller_test.rb | The functional tests for the controller  |
| app/helpers/comments_helper.rb              | A view helper file                       |
| test/unit/helpers/comments_helper_test.rb   | The unit tests for the helper            |
| app/assets/javascripts/comment.js.coffee    | CoffeeScript for the controller          |
| app/assets/stylesheets/comment.css.scss     | Cascading style sheet for the controller |

Like with any blog, our readers will create their comments directly after
reading the post, and once they have added their comment, will be sent back to
the post show page to see their comment now listed. Due to this, our
`CommentsController` is there to provide a method to create comments and delete
spam comments when they arrive.

So first, we'll wire up the Post show template
(`/app/views/posts/show.html.erb`) to let us make a new comment:

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

This adds a form on the `Post` show page that creates a new comment by
calling the `CommentsController` `create` action. The `form_for` call here uses
an array, which will build a nested route, such as `/posts/1/comments`.

Let's wire up the `create`:

```ruby
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(params[:comment])
    redirect_to post_path(@post)
  end
end
```

You'll see a bit more complexity here than you did in the controller for posts.
That's a side-effect of the nesting that you've set up. Each request for a
comment has to keep track of the post to which the comment is attached, thus the
initial call to the `find` method of the `Post` model to get the post in question.

In addition, the code takes advantage of some of the methods available for an
association. We use the `create` method on `@post.comments` to create and save
the comment. This will automatically link the comment so that it belongs to that
particular post.

Once we have made the new comment, we send the user back to the original post
using the `post_path(@post)` helper. As we have already seen, this calls the
`show` action of the `PostsController` which in turn renders the `show.html.erb`
template. This is where we want the comment to show, so let's add that to the
`app/views/posts/show.html.erb`.

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

Now you can add posts and comments to your blog and have them show up in the
right places.

![Post with Comments](http://edgeguides.rubyonrails.org/images/getting_started/post_with_comments.png)

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
