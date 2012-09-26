Introducción a Rails
====================

Este proyecto nace con la idea de traducir al español la guía oficial
["Getting Started with Rails"](http://guides.rubyonrails.org/getting_started.html).

Esta guía cubre ¿cómo comenzar con Ruby on Rails? Luego de leerla, aprenderás
lo siguiente:

* Instalar Rails, crear una nueva aplicación Rails y conectar tu aplicación a
  una base de datos.
* La estructura general de una aplicación Rails.
* Los principios básicos del patrón MVC (Modelo, Vista, Controlador) y
  Diseño RESTful.
* Como generar rápidamente las primeras piezas de una aplicación Rails.

--------------------------------------------------------------------------------

WARNING. Esta guía está basada en Rails 3.2. Algunas partes del código que
se muestran aquí no van a funcionar en nuevas versiones de Rails.

Antes de Empezar
----------------

Esta guía está diseñada para principiantes que quieren comenzar con Rails
desde cero. No asume que tú tienes alguna experiencia previa con Rails. Sin
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
Ruby on Rails de una manera rápida. En nuestro [wiki](https://github.com/rubyperu/rubyperu.github.com/wiki)
encontrarás información acerca de cómo instalar Ruby y Ruby on Rails.

Para verificar que tu instalación esté correcta, deberías
poder correr lo siguiente:

```bash
$ rails --version
```

Si dice algo como "Rails 3.2", estás listo para continuar.

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

Poniendo todo en funcionamiento
-------------------------------

Ahora que has visto como crear un controlador, una acción y una vista, vamos a crear
algo con un poco más de sentido.

En la aplicación de Blog, tú vas a crear un nuevo recurso (_resource_). Un recurso
es el término usado para una colección de objetos similares, como posts, personas o
animales. Tú puedes crear, leer, actualizar y eliminar objetos para un recurso
y estas operaciones son referedidas como operaciones _CRUD_.

En la siguiente sección, tú añadirás la habilidad de crear nuevos posts en tu aplicación
y poder verlos también. Ésto es la "C" y la "R" de _CRUD_: creación y lectura. La manera
de hacer esto se vería de la siguiente manera:

![The new post form](http://edgeguides.rubyonrails.org/images/getting_started/new_post.png)

Se ve un poco básico por ahora, pero está bien. Ya veremos como mejorar el estilo.

Estableciendo la base
---------------------

La primera cosa que necesitaremos para crear un nuevo post, es crear un espacio para hacer eso
en nuestra aplicación. Un buen lugar podría ser `/posts/new`. Si tratas de navegar a esa
dirección ahora -- visitando <http://localhost:3000/posts/new> -- Rails te dará un error de
ruteo:

![A routing error, no route matches /posts/new](http://edgeguides.rubyonrails.org/images/getting_started/routing_error_no_route_matches.png)

Esto es porque no en ningún lucar dentro de las rutas para la aplicación -- definidas dentro
de `config/routes.rb` -- que defina esta ruta. Por defecto, Rails no tiene rutas configuradas,
excepto por la ruta `root` que definimos anteriormente, es por esto que tú tendrás que definir
tus rutas cuando las necesites.

Para hacer esto, vas a necesitar crear una ruta dentro de el archivo `config/routes.rb`, en
una nueva línea entre el `do` y el `end` del método `draw`:

```ruby
get "posts/new"
```

Esta ruta es super simple: define una nueva ruta que sólo responderá a peticiones `GET`, y qye
la ruta se encuentra en `posts/new`. Pero como sabe a donde ir sin haber usado la opción
`:to`? Bueno, Rails usa una convención sensible aquí: Rails asumirá que lo que tú quieres
es que esta ruta vaya a la acción `new` dentro de el controlador `posts`.

Con esta ruta definidad, tus peticiones ahora se pueden hacer a través de `/posts/new` en
la aplicación. Navega hacia: <http://localhost:3000/posts/new>. Verás otro error de ruteo:

![Another routing error, uninitialized constant PostsController](http://edgeguides.rubyonrails.org/images/getting_started/routing_error_no_controller.png)

Este error está pasando porque esta ruta necesita un controlador que esté definido. La ruta
está tratando de encontrar el controlador para servir la petición, pero con el controlador
no definido, simplemente no lo puede hacer. La solución para este caso en particular es simple:
crea un controllador llamado `PostsController`. Puedes hacerlo ejecutando el siguiente comando:

```bash
$ rails g controller posts
```

Si abres el nuevo archivo generado `app/controllers/posts_controller.rb`,
verás un controlador vacío:

```ruby
class PostsController < ApplicationController
end
```

Un controlador es simple una clase que es definida para heredar de `ApplicationController`.
Dentro de ésta, vas a definir los métodos que se convertirán en acciones para este controlador.
Estas acciones van a ejecutar operaciones _CRUD_ sobre los posts dentro de nuestro sistema.

Si refrescas la dirección <http://localhost:3000/posts/new> ahora, vas a tener un nuevo error:

![Unknown action new for PostsController!](http://edgeguides.rubyonrails.org/images/getting_started/unknown_action_new_for_posts.png)

Este error indica que Rails no puede encontrar la acción `new` dentro de
`PostsController` que recién has generado. Esto es porque cuando los controladores
son generados en Rails están vacíos por defecto, a menos que le digas que acciones
quieres durante el proceso de generación.

Para definir manualmente una acción dentro de un controlador, todo lo que necesitas
es definir un nuevo método dentro del controlador. Abre `app/controllers/posts_controller.rb`
y dentro de la clase `PostsController`, define el método `new` así:

```ruby
def new
end
```

Con el método `new` definido en `PostsController`, si tú refrescas
<http://localhost:3000/posts/new> verás otro error:

![Template is missing for posts/new](http://edgeguides.rubyonrails.org/images/getting_started/template_is_missing_posts_new.png)

Estás obteniendo este error ahora porque Rails espera que las acciones planas
como ésta tengan vistas asociadas a ellas para mostrar la información. Con ninguna
vista disponible, Rails mostrará un error.

En la imagen de arriba, la línea de abajo fue eliminada. Vamos a ver como se el error completo:

<blockquote>
Missing template posts/new, application/new with {:locale=>[:en], :formats=>[:html], :handlers=>[:erb, :builder, :coffee]}. Searched in: * "/path/to/blog/app/views"
</blockquote>

Eso es casi un montón de texto! Revisemos rápidamente para entender cuál es la función de cada parte.

La primera parte identifica que plantilla está faltando. En este caso, es la plantila `posts/new`.
Rails primero buscará esta plantilla. Si no la encuentra, luego tratará de cargar la plantilla
llamada `application/new`. Busca una aquí porque el `PostsController` hereda de `ApplicationController`.

La siguiente parte del mensaje contiene un map (`hash` en inglés). La llave `:locale` en este map
simplemente indica el lenguaje que debe contener la plantilla solicitada. Por defecto, está configurado
en Inglés -- o "en" --. La siguiente llave, `:formats` especifica el formato de la plantilla que será
servido en la respuesta. El formato por defecto es `:html`, es por eso que Rails busca una plantilla
HTML. La llave final, `:handlers`, nos dice que _manejador de plantilla_ (o _template handler_ en inglés)
puede ser usada para producir nuestra plantilla. `:erb` es el manejador más usado para plantillas HTML,
`:builder` es usado para plantillas XML, y `:coffee` usa CoffeeScript para construir plantillas JavaScript.

La más simple plantilla que funcionaría en nuestro caso sería una localizada en `app/views/posts/new.html.erb`.
La extensión de este nombre de archivo es importante: la primera extensión define el _formato_ de la plantilla,
y la segunda extensión el _manejador de plantilla_ que será usado. Rails está tratando de encontrar una
plantilla llamada `posts/new` en `app/views` para la aplicación. El formato para esta plantilla puede sólo
ser `html` y el manejador debería ser `erb`, `builder` o `coffee`. Ya que tú quieres crear un nuevo
formulario HTML, tú tendrás que usar el lenguaje `ERB`. Por lo tanto el archivo debería ser llamado
`posts/new.html.erb` y necesita ser localizado dentro de la carpeta `app/views` de la aplicación.

Ahora ve y crea un nuevo archivo en `app/views/posts/new.html.erb` y escribe el siguiente
contenido en él:

```html
<h1>New Post</h1>
```

Cuando refresques <http://localhost:3000/posts/new>, verás que la página tiene un título. La ruta,
el controlador, la acción y la vista ahora están funcionando de manera armoniosa! Es hora de crear
el formulario para un nuevo post.

The first form
--------------

Para crear una formulario con esta plantilla usarás un _constructor de formularios_ (o _form builder_
en inglés). El form builder primario de Rails está provisto por un método de ayuda llamado `form_for`.
Para usar este método agrega este código a `app/views/posts/new.html.erb`:

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

Si refrescas la página ahora, verás el mismo formulario que en el ejemplo.
Construir un formulario en Rails es así de sencillo!

Cuando llamas a `form_for`, le pasas un objeto identificador para este
formulario. En este caso, es el símbolo `:post`. Esto le indica al método
`form_for` para quién es este formulario. Dentro del bloque para este método,
el objeto `FormBuilder` - representado por `f` - es usado para construir dos
etiquetas y dos cajas de texto, una de cada una para el título y el texto del
post. Finalmente, la llamada al método `submit` en el objeto `f` creará un
botón de submit en el formulario.

Sin embargo, existe un problema con este formulario. Si inspeccionas el código
HTML generado, al ver la fuente de la página, verás que el atributo `action` de
el formulario apunta a `/posts/new`. Ésto es un problema debido a que esta ruta
va a la misma página donde te encuentras en este momento cuando en realidad la
ruta debería sólo ser usada para mostrar el formulario para un nuevo post.

El formulario necesita usar un URL distinto para poder dirigirse hacia algún otro
lugar. Ésto puede hacerse, de manera bastante sencilla, con la opción `:url` de
`form_for`. En Rails la acción que se usa típicamente para nuevas entradas es llamada
"create" (crear en español) por lo que el formulario debería ser apuntado hacia
esa acción.

Edita la linea de `form_for` siguiente: `app/views/posts/new.html.erb` para que
se vea así:

```html+erb
<%= form_for :post, :url => { :action => :create } do |f| %>
```

En este ejemplo un objeto `Hash` es pasado a la opción `:url`. Lo que Rails hará con
esto es apuntar el formulario a la acción `create` de el controlador actual, el `PostsController`.
y enviará una petición de `POST` hacia esa ruta. Para que esto funcione necesitarás añadir
una ruta a `config/routes.rb`, justo debajo de la de "post/new":

```ruby
post "posts" => "posts#create"
```

Al usar el método `post` en vez de `get`, Rails definirá una ruta que solo responderá a metodos POST.
El método POST es el método típico utilizado por todos los formularios a lo largo de la red.

Con el formulario y su ruta asociada definidas, serás capaz de llenar el formulario y dar click en el
botón de submit para empezar el proceso de creación de un nuevo post, así que ve y haz eso. Cuando
des click al botón y envíes el formulario, te encontrarás con un error familiar.

![Unknown action create for PostsController](http://edgeguides.rubyonrails.org/images/getting_started/unknown_action_create_for_posts.png)

Ahora necesitas crear la acción `create` en `PostsController` para que funcione.

### Creando artículos

Para hacer que "Unknown action" desaparezca, puedes definir una acción `create`
dentro de la clase `PostsController` en `app/controllers/posts_controller.rb`, debajo de la acción `new`:

```ruby
class PostsController < ApplicationController
  def new
  end

  def create
  end

end
```

Si reenvías el formulario ahora, verás otro error común: falta una plantilla. Está bien, vamos a ignorar
eso por ahora. Lo que la acción `create` debe hacer es salvar el nuevo artículo en la base de datos.

Cuando un formulario es enviado, los campos del formulario son enviados a Rails como _parámetros_. Estos
parámetros pueden ser referenciados dentro de las acciones del controlador, generalmente para realizar una
tarea determinada. Para ver que hacen estos parámetros, cambiar la acción `create` a esto:

```ruby
def create
  render :text => params[:post].inspect
end
```

El método `render` toma un simple hash con la clave `text` y el valor de `params[:post].inspect`. El
método `params` es el objeto que representa a los parámetros (o campos) que vienen desde el formulario.
El método `params` retorna un objeto `HashWithIndifferentAccess`, que te permite acceder a las claves del hash
usando cadenas o símbolos. En esta situación los únicos parámetros que importan son los que vienen del
formulario.

Si reenvias el formulario una vez más, ya no obtendrás el error de plantilla faltante, en su lugar verás
algo como lo que sigue:

```ruby
{"title"=>"First post!", "text"=>"This is my first post."}
```

Esta acción muestra ahora los parámetros para el artículo que están llegando desde el formulario. Sin
embargo, esto no es realmente útil. Sí, puedes ver los parámetros, pero no hay nada en particular que se
está haciendo con ellos.

### Creando el modelo post

Los modelos en Rails usan un nombre en singular, y sus correspondientes tablas
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

CONSEJO: Active Record es lo suficientemente inteligente para asignar
automáticamente el nombre de las columnas a atributos del modelo,
lo que significa que tú no tienes que declarar los atributos dentro
de los modelos de Rails, ya que será realizado automáticamente por
Active Record.

### Ejecutando una migración

Como hemos visto, `rails generate model` crea un archivo _database
migration_ dentro del directorio `db/migrate`.
Migraciones son clases de Ruby que están diseñadas para hacer simple la
creación y modificación de las tablas de la base de datos. Rails usa comandos rake
para ejecutar migraciones, y es posible deshacer una migración despues que ha sido aplicada
a la base de datos. Archivo de migraciones incluyen una marca de la fecha y hora para
que sean procesadas en el orden que fueron creadas.

Si miras dentro del archivo `db/migrate/20120419084633_create_posts.rb` (recuerda,
tu archivo puede tener un nombre ligeramente diferente), esto es lo que encontrarás:

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

La migración de arriba crea un método llamado `change` el cual será llamado cuando ejecutes
la migración. La acción definida en este método es reversible, lo cual significa que Rails
conoce como deshacer los cambios realizados en esta migración en caso que necesites hacer eso
más tarde. Cuando ejecutas esta migración se creará una tabla `post` con una columna tipo `string`
y otra columna tipo `text`. También crea dos campos de fecha-hora para permitir a Rails realizar
un seguimiento de las actualizaciones. Mayor información acerca de las migraciones en Rails
pueden ser encontradas en la guía [Rails Database Migrations](http://guides.rubyonrails.org/migrations.html).

En este punto, puedes usar el comando rake para ejecutar la migración:

```bash
$ rake db:migrate
```

Rails ejecutará este comando de migración y te responderá lo siguiente cuando haya
creado la tabla `Posts`.

```bash
==  CreatePosts: migrating ====================================================
-- create_table(:posts)
   -> 0.0019s
==  CreatePosts: migrated (0.0020s) ===========================================
```

NOTA. Debido a que estás trabajando en el ambiente de desarrollo por omisión,
este comando se aplicará a la base de datos definida en la sección `development`
de tu archivo `config/database.yml`. Si deseas ejecutar migraciones en otro
ambiente, por ejemplo en producción, debes indicarlo en forma explícita cuando
invoques el comando: `rake db:migrate RAILS_ENV=production`.

### Salvando datos en el controlador

En `posts_controller` necesitamos cambiar la acción `create` para usar el nuevo modelo `Post`
y guardar los datos en la base de datos. Abra el archivo y cambie la acción `create`
que debe verse de la siguiente manera:

```ruby
def create
  @post = Post.new(params[:post])

  @post.save
  redirect_to :action => :show, :id => @post.id
end
```

Esto es lo que sucede: cada modelo Rails puede ser inicializado con sus respectivos
atributos, los cuales son automáticamente asignados a sus respectivas columnas de
base de datos. En la primera línea hacemos justamente eso (recuerda que
`params[:post]` contiene los atributos en los cuales estamos interesados). Luego,
`@post.save` es responsible de guardar el modelo en la base de datos. Finalmente,
direccionamos al usuario a la acción `show` que definiremos más tarde.

CONSEJO: Como veremos más tarde, `@post.save` devuelve un indicador que indica si el
modelo fue guardado o no.

### Mostrando artículos

Si envías el formulario de nuevo, Rails se quejará que no has definido la acción `show`.
Esto no es muy útil así que vamos a agregar la acción `show` antes de continuar. Abra
el archivo `config/routes.rb` y agregue la siguiente ruta:

```ruby
get "posts/:id" => "posts#show"
```

La sintaxis especial `:id` le dice a Rails que la ruta espera un parámetro `:id`,
el cual en nuestro caso será el id del artículo. Note que en esta ocasión
debemos indicar la asignación real `posts#show` porque de otra manera Rails no sabrá
que acción debe realizar.

Como dijimos anteriormente, necesitamos agregar la acción `show` en el `posts_controller`
y su respectiva vista.

```ruby
def show
  @post = Post.find(params[:id])
end
```

Un par de cosas a tener en cuenta. Usamos `Post.find` para encontrar el artículo en el
cual estamos interesados. También usamos una variable de instancia (con el prefijo @)
para contener una referencia al objeto `post`. Hacemos eso porque Rails pasará todas
las variables de instancia a la vista.

Ahora, crea un nuevo archivo `app/view/posts/show.html.erb` con el siguiente contenido:

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

Finalmente, si vas a
[http://localhost:3000/posts/new](http://localhost:3000/posts/new) serás capaz de
crear un artículo. ¡Inténtalo!

![Show action for posts](http://edgeguides.rubyonrails.org/images/getting_started/show_action_for_posts.png)

### Listando todos los artículos

Aún necesitamos una forma de listar todos los artículos, de manera que vamos a hacerlo.
Como de costumbre, vamos a necesitar una ruta ubicada dentro de `config/routes.rb`:

```ruby
get "posts" => "posts#index"
```

Y una acción para esa ruta dentro de `PostsController` en el archivo `app/controllers/posts_controller.rb`:

```ruby
def index
  @posts = Post.all
end
```

Y finalmente una vista para esta acción, ubicada en `app/views/posts/index.html.erb`:

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

Ahora si vamos a `http://localhost:3000/posts` veremos una lista con todos los artículos que has creado.

### Agregando enlaces

Hasta el momento puedes crear, mostrar y listar artículos. Ahora vamos a agregar
algunos enlaces para navegar a través de las páginas.

Abra `app/views/welcome/index.html.erb` y modifiquelo como se indica a continuación:

```html+erb
<h1>Hello, Rails!</h1>
<%= link_to "My Blog", :controller => "posts" %>
```

El método `link_to` es uno de los asistentes de la vista incorporados en Rails. Este método crea el
hipervínculo mostrando un texto e indicando donde irá, en este caso a la ubicación `post`.

Vamos a agregar enlaces a las otras vistas, empezando por agregar a "New Post" el enlace a
`app/views/posts/index.html.erb`, ubicándola encima de `<!-- <table> -->` tag:

```erb
<%= link_to 'New post', :action => :new %>
```

Este enlace te permitirá abrir el formulario para crear un nuevo artículo. También deberías
agregar un enlace a esta plantilla -- `app/views/posts/new.html.erb` -- para regresar a la
acción `index`. Para hacer eso agregue el enlace debajo del formulario en esta plantilla:

```erb
<%= form_for :post do |f| %>
  ...
<% end %>

<%= link_to 'Back', :action => :index %>
```

Finalmente, agregue otro enlace a la plantilla `app/views/posts/show.html.erb` para regresar
a la acción `index`, de manera que la persona que está viendo un artículo pueda regresar
y ver la lista completa nuevamente.

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

CONSEJO: Si deseas crear un enlace a una acción dentro del mismo controlador
no necesitas especificar la opción `:controller`, Rails usará el actual
controlador por omisión.

CONSEJO: En modo de desarrollo (en la cual estás trabajdo por omisión), Rails recarga
tu aplicación en cada requerimiento del navegador, por lo que no hay necesidad de
reiniciar el servidor web cuando un cambio es realizado.

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

### Usando parciales para eliminar la duplicidad en las vistas

`partials` son lo que Rails usa para remover la duplicidad en las vistas. Aquí hay
un ejemplo:

```html+erb
# app/views/user/show.html.erb

<h1><%= @user.name %></h1>

<%= render 'user_details' %>

# app/views/user/_user_details.html.erb

<%= @user.location %>

<%= @user.about_me %>
```

La plantilla `users/show` automáticamente incluirá el contenido de la plantilla
`users/_user_details`. Nota que los parciales tienen como prefijo un subrayado,
de manera de no confundirlas con vistas regulares. Sin embargo, no incluyas
el subrayado cuando las incluyas dentro del método `helper`.

CONSEJO: Puedes leer más acerca de parciales en la guía
[Layouts and Rendering in Rails](layouts_and_rendering.html).

Nuestra acción `edit` parece muy similar a la acción `new`, en efecto ellos
comparten el mismo código para mostrar el formulario. Vamos a limpiarlo
usando un parcial.

Crea un nuevo archivo `app/views/posts/_form.html.erb` con el siguiente contenido:

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

Todo, excepto la declaración `form_for` permanece igual. Como `form_for`
puede averiguar la `action` y los atributos del `method` correcto
cuando construye el formulario será explicado eun unos momentos.
Por ahora, vamos a actualizar la vista
`app/views/posts/new.html.erb` para usar el nuevo parcial, reescribiendo completamente:

```html+erb
<h1>New post</h1>

<%= render 'form' %>

<%= link_to 'Back', :action => :index %>
```

Luego hacer lo mismo a la vista `app/views/posts/edit.html.erb`:

```html+erb
<h1>Edit post</h1>

<%= render 'form' %>

<%= link_to 'Back', :action => :index %>
```

Ve con tu navegador a [http://localhost:3000/posts/new](http://localhost:3000/posts/new) y
trata de crear un nuevo artículo. Todo funciona todavía, Ahora tratemos de editar el
artículo y recibiremos el siguiente mensaje de error:

![Undefined method post_path](http://edgeguides.rubyonrails.org/images/getting_started/undefined_method_post_path.png)

Para entender este error necesitamos conocer como funciona `form_for`.
Cuando pasas un objeto a `form_for` y no especificas la opción de `:url`,
Rails trata de adivinar las opciones de `action` y `method` verificando
si el objeto pasado es un nuevo registro o no. Rails sigue la convencion
REST, de esta manera si se está creando un nuevo objeto `Post` buscará por una
ruta llamada `post_path` y para actualizar un objeto `Post` buscará por una
ruta llamada `post_path` y le pasará el objeto actual. Similarmente, Rails conoce
que debe crear nuevos objetos a través de POST y actualizarlos a través de PUT.

Si ejecutas `rake routes` desde la consola verás que ya tenemos una ruta
`posts_path`, la cual fue creada automáticamente por Rails cuando se definió la ruta
por la acción `index`. Sin embargo, no tenemos aún un `post_path`, la cual es la
razón por la quje recibimos el error anterior.

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

Para arreglar eso, abrimos el archivo `config/routes.rb` y modificamos la línea `get "posts/:id"`
a esto:

```ruby
get "posts/:id" => "posts#show", :as => :post
```

La opción `:as` le dice al método `get` que queremos hacer que los asistentes
de ruteo llamados `post_url` y `post_path` estén disponibles para nuestra aplicación.
Estos son los métodos que `form_for` necesita cuando estamos editando un artículo y que ahora
están disponibles para actualizar los artículos.

NOTA: La opción `:as` esta disponible también en los métodos de ruteo
`post`, `put`, `delete` y `match`.

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
