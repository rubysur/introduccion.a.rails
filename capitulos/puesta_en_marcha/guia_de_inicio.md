¿Qué es Rails?
==============

Rails es un framework de desarrollo de aplicaciones web escrito en el
lenguaje de programación Ruby. Está diseñado para hacer que la programación
de aplicaciones web sea más fácil, haciendo supuestos sobre lo que cada
desarrollador necesita para comenzar. Te permite escribir menos código
realizando más que muchos otros lenguajes y frameworks. Además, expertos
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

Creando un nuevo proyecto
=========================

La mejor forma de usar esta guía es seguir cada paso como es el caso, no hay
ningún código o paso para hacer este ejemplo de aplicación que haya quedado
fuera, así que puedes literalmente seguirla paso a paso.

Al seguir esta guía, tú vas a crear un proyecto Rails llamado `blog`, un (muy)
simple weblog. Antes de que puedas comenzar a crear la aplicación, necesitas
estar seguro de tener Rails instalado.

> **TIP:** Los ejemplos que se muestran a continuación usan `$` para denotar un
superuser y user regular de una línea de comandos respectivamente en un sistema
operativo tipo UNIX. Si estás usando Windows, tu línea de comandos se verá como
`c:\source_code>`.

Instalando Rails
================

Para instalar Rails, usa el comando proporcionado por RubyGems `gem install`:

```bash
# gem install rails
```

> **TIP:** Existen un número de herramientas que te ayudarán a instalar Ruby y
Ruby on Rails de una manera rápida. En el [wiki de Ruby Perú](https://github.com/rubyperu/rubyperu.github.com/wiki)
encontrarás información acerca de cómo instalar Ruby y Ruby on Rails.

Para verificar que tu instalación está correcta, deberías
poder correr lo siguiente:

```bash
$ rails --version
```

Si dice algo como "Rails 5.0.0", estás listo para continuar.

Creando la aplicación de Blog
-----------------------------

Rails viene con un número de generadores que están diseñados para hacer tu ciclo
de desarrollo más fácil. Uno de esos es el generador de nuevas aplicaciones, el
cual te proveerá con la estructura base de una aplicación Rails, así ya no
tienes que escribirla por ti mismo.

Para usar este generador, abre la terminal, navega hacia el directorio en donde
tienes permiso para crear archivos, y escribe:

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
|bin/|Contiene el script de Rails que inicia tu aplicación y contiene otros scripts usados para desplegar o correr tu aplicación.|
|config/|Configura las reglas de ejecución de la aplicación, rutas, base de datos y más. Este tema es cubierto en mayor detalle en [Configuring Rails Applications](http://edgeguides.rubyonrails.org/configuring.html).|
|config.ru| Configuración Rack para servidores basados en Rack usados para iniciar la aplicación.|
|db/|Contiene el esquema actual de tu base de datos, así como las migraciones de la base de datos.|
|doc/|Documentación detallada de tu aplicación.|
|Gemfile<br />Gemfile.lock| Estos arhivos te permiten especificar qué dependencias de gemas son necesitadas para tu aplicación Rails. Estos archivos son usados por la gema Bundler, ver [Sitio web de Bundler](http://gembundler.com).|
|lib/|Módulos extendidos para tu aplicación.|
|log/|Archivos de Log de tu aplicación.|
|public/|La única carpeta vista por el mundo tal como es. Contiene los archivos estáticos y assets compilados.|
|Rakefile|Este archivo localiza y carga tareas que pueden ser ejecutadas desde la línea de comandos. La lista de tareas son definidas a través de los componentes de Rails. En vez de cambiar el Rakefile, deberías agregar tus propias tareas, añadiendo archivos al directorio `lib/tasks` de tu aplicación.|
|README.rdoc|Este es un breve manual de instrucciones para tu aplicación. Deberías editar este archivo para comunicar a otros lo que tu aplicación hace, cómo configurarla y demás.|
|test/|Pruebas unitarias, fixtures y otras pruebas. Éstos son cubiertos en [Testing Rails Applications](http://edgeguides.rubyonrails.org/testing.html).|
|tmp/|Archivos temporales (como archivos de caché, pid y archivos de sesiones).|
|vendor/|Lugar para código de terceros. En una típica aplicación Rails, esta incluye librerías y plugins.|

Hola, Rails!
============

Para comenzar, vamos a obtener un poco de texto en la pantalla rápidamente. Para
hacer ésto, necesitas tener tu servidor de aplicación Rails corriendo.

Iniciando el Servidor Web
=========================

En realidad ya tienes una aplicación Rails funcional, Para verla, necesitas
iniciar un servidor web en tu máquina de desarrollo. Puedes hacerlo ejecutando:

```bash
$ rails server
```

> **TIP:** Compilando CoffeeScript a JavaScript requiere un JavaScript runtime y la
ausencia de éste dará un error de `execjs`. Usualmente Mac OS X y Windows vienen
con un Javascript runtime instalado. Rails agrega la gema `therubyracer` al
`Gemfile` en una línea comentada para nuevas aplicaciones y puedes descomentarla
si la necesitas. `therubyrhino` es el runtime recomendado para usuarios de JRuby
y es añadido por defecto al `Gemfile` en aplicaciones generadas bajo JRuby.
Puedes investigar acerca de todos los runtimes soportados en
[ExecJS](https://github.com/sstephenson/execjs#readme).

Esto lanzará WEBrick, un servidor web incorporado en Ruby por defecto. Para ver
tu aplicación en acción, abre tu navegador preferido e ingresa a [http://localhost:3000](http://localhost:3000).
Deberías ver la página de información por defecto de Rails.

![Welcome Aboard screenshot](http://guides.rubyonrails.org/images/getting_started/rails_welcome.png)

> **TIP:** Para detener el servidor web, presiona Ctrl+C en la ventana de la línea
de comandos donde se está ejecutando. En modo de desarrollo, Rails generalmente
no requiere reiniciar el servidor web; los cambios realizados serán tomados
automáticamente por el servidor.

La página "Welcome Aboard" es la primera prueba para una nueva aplicación Rails:
Ésta asegura que tienes el software configurado correctamente para servir una página.
También puedes hacer click en el link _About your application's enviroment_ para ver
un resumen del entorno de tu aplicación.

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
lenguaje llamado _eRuby_ (Embedded Ruby), el cual es convertido por cada ciclo
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
invoke  assets
invoke    coffee
create      app/assets/javascripts/welcome.coffee
invoke    scss
create      app/assets/stylesheets/welcome.scss
```

Los más importantes de éstos son por supuesto el controlador, localizado en
`app/controllers/welcome_controller.rb` y la vista, localizada en
`app/views/welcome/index.html.erb`.

Abre el archivo `app/views/welcome/index.html.erb` en tu editor de texto
y edítalo para que contenga sólo está línea de código:

```html
<h1>Hello, Rails!</h1>
```

Estableciendo la página principal
=================================

Ahora que hemos hecho el _controlador_ y la _vista_, necesitamos decirle a Rails
cuándo queremos que `Hello Rails` se muestre. En nuestro caso, deseamos mostrarlo
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

Abre el archivo `config/routes.rb` en tu editor.

```ruby
Rails::Application.routes.draw do
  get "welcome/index"

  # The priority is based upon order of creation:
  # first created -> highest priority.
  # ...
  # You can have the root of your site routed with "root"
  # just remember to delete public/index.html.
  # root :to => "welcome#index"
```

Éste es el _archivo de enrutamiento_ de tu aplicación el cual mantiene entradas
con un DSL especial (domain-specific language) que le dicen a Rails cómo conectar
peticiones entrantes a _controladores_ y _acciones_. Este archivo contiene muchas
rutas de ejemplo en líneas comentadas, y una de ellas en realidad muestra como
conectar la raíz de tu sitio a un _controlador_ y _acción_ específico. Encuentra
la línea iniciando con `root :to` y descoméntala. Debería verse como lo siguiente:

```ruby
Rails::Application.routes.draw do
  get "welcome/index"

  root "welcome#index"
```

El `root "welcome#index"` le indica a Rails mapear peticiones de la raíz
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

> **NOTA:** Para mayor información acerca del enrutamiento, ir a
[Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html).

Creando un nuevo post
=====================

Ahora que has visto cómo crear un controlador, una acción y una vista, vamos a crear
algo con un poco más de sentido.

En la aplicación de Blog, tú vas a crear un nuevo recurso (_resource_). Un recurso
es el término usado para una colección de objetos similares, como posts, personas o
animales. Tú puedes crear, leer, actualizar y eliminar objetos para un recurso
y estas operaciones son referidas como operaciones _CRUD_.

Rails proporciona un método (_resource_) que se puede utilizar para declarar un recurso REST estándar.
Es necesario agregar el recurso (_article_) en `config/routes.rb` el archivo se verá de la siguiente manera:

```ruby
Blog.application.routes.draw do
  resources :articles

  root 'welcome#index'
end
```
Si ejecutas `rails routes` veras que se han definido rutas para todas las acciones estandar de RESTful.
El significado de la columna _prefix_ (y otras columnas) los veremos mas adelante, lo importante es notar
que Rails ha inferido la palabra en singular del recurso articles es article, con lo que el resultado es el siguiente:

```bash
$ bin/rails routes
      Prefix Verb   URI Pattern                  Controller#Action
    articles GET    /articles(.:format)          articles#index
             POST   /articles(.:format)          articles#create
 new_article GET    /articles/new(.:format)      articles#new
edit_article GET    /articles/:id/edit(.:format) articles#edit
     article GET    /articles/:id(.:format)      articles#show
             PATCH  /articles/:id(.:format)      articles#update
             PUT    /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy
        root GET    /                            welcome#index
```

En la siguiente sección, tú añadirás la habilidad de crear nuevos posts en tu aplicación
y poder verlos también. Ésto es la "C" y la "R" de _CRUD_: creación y lectura. La manera
de hacer esto se vería de la siguiente manera:

![The new post form](http://guides.rubyonrails.org/images/getting_started/new_article.png)

Se ve un poco básico por ahora, pero está bien. Ya veremos cómo mejorar el estilo.

Estableciendo la base
=====================

La primera cosa que necesitaremos para crear un nuevo post, es crear un espacio
en nuestra aplicación. Un buen lugar podría ser `/articles/new`. Si tratas de navegar a esa
dirección ahora -- visitando <http://localhost:3000/articles/new> -- Rails te dará un error de
ruteo:

![A routing error, no route matches /articles/new](http://guides.rubyonrails.org/images/getting_started/routing_error_no_controller.png)

Este error se produce porque la ruta tiene que tener un controlador definido con el fin de atender la solicitud. La solución a este problema es simple: crear un controlador llamado `ArticlesController`.Podemos hacer esto mediante la ejecución de este comando:

```bash
rails generate controller Articles
```

Si abres el nuevo archivo generado `app/controllers/articles_controller.rb`,
verás un controlador vacío:

```ruby
class ArticlesController < ApplicationController
end
```

Un controlador es simplemente una clase que es definida para heredar de `ApplicationController`.
Dentro de ésta, vas a definir los métodos que se convertirán en acciones para este controlador.
Estas acciones van a ejecutar operaciones _CRUD_ sobre los posts dentro de nuestro sistema.

Si refrescas la dirección <http://localhost:3000/articles/new> ahora, vas a tener un nuevo error:

![Unknown action new for PostsController!](http://guides.rubyonrails.org/images/getting_started/unknown_action_new_for_articles.png)

Este error indica que Rails no puede encontrar la acción `new` dentro de
`ArticlesController` que recién has generado. Esto es porque cuando los controladores
son generados en Rails están vacíos por defecto, a menos que le digas que acciones
quieres durante el proceso de generación.

Para definir manualmente una acción dentro de un controlador, todo lo que necesitas
es definir un nuevo método dentro del controlador. Abre `app/controllers/articles_controller.rb`
y dentro de la clase `ArticlesController`, define el método `new` así:

```ruby
class ArticlesController < ApplicationController
  def new
  end
end
```

Con el método `new` definido en `ArticlesController`, si actualizas
<http://localhost:3000/articles/new> verás otro error:

![Template is missing for posts/new](http://guides.rubyonrails.org/images/getting_started/template_is_missing_articles_new.png)

Estás obteniendo este error ahora porque Rails espera que las acciones planas
como ésta tengan vistas asociadas a ellas para mostrar la información. Con ninguna
vista disponible, Rails mostrará un error.

En la imagen de arriba, la línea de abajo fue eliminada. Vamos a ver como se ve el error completo:

<blockquote>
ArticlesController#new is missing a template for this request format and variant. request.formats: ["text/html"] request.variant: [] NOTE! For XHR/Ajax or API requests, this action would normally respond with 204 No Content: an empty white screen. Since you're loading it in a web browser, we assume that you expected to actually render a template, not… nothing, so we're showing an error to be extra-clear. If you expect 204 No Content, carry on. That's what you'll get from an XHR or API request. Give it a shot.
</blockquote>

Eso es casi un montón de texto! Revisemos rápidamente para entender cuál es la función de cada parte.

La primera parte identifica que plantilla está faltando. En este caso, es la plantila `articles/new`.
Rails primero buscará esta plantilla, si no la encuentra, tratará luego de cargar la plantilla
llamada `application/new`. Busca una aquí porque el `ArticlesController` hereda de `ApplicationController`.

La siguiente parte del mensaje contiene un map (`hash` en inglés). La clave `:locale` en este map
simplemente indica el lenguaje que debe contener la plantilla solicitada. Por defecto, está configurado
en Inglés -- o "en" --. La siguiente clave, `:formats` especifica el formato de la plantilla que será
servido en la respuesta. El formato por defecto es `:html`, es por eso que Rails busca una plantilla
HTML. La clave final, `:handlers`, nos dice que _manejador de plantilla_ (o _template handler_ en inglés)
puede ser usada para producir nuestra plantilla. `:erb` es el manejador más usado para plantillas HTML,
`:builder` es usado para plantillas XML, y `:coffee` utiliza CoffeeScript para construir plantillas JavaScript.

El mensaje también contiene `request.formats` que especifica el formato de la plantilla que se sirve en la respuesta. Se establece `text/html` como solicitamos esta página a través del navegador, por lo que Rails está buscando una plantilla HTML.

La más simple plantilla que funcionaría en nuestro caso sería una localizada en `app/views/articles/new.html.erb`. La extensión de este nombre de archivo es importante: la primera extensión define el _formato_ de la plantilla, y la segunda extensión el _manejador de plantilla_ que será usado. Rails está tratando de encontrar una plantilla llamada `articles/new` en `app/views` para la aplicación. El formato para esta plantilla puede sólo ser `html` y el manejador debería ser `erb`, `builder` o `coffee`.

Ya que tú quieres crear un nuevo formulario HTML, tendrás que usar el lenguaje `ERB`. Por lo tanto el archivo debería ser llamado `articles/new.html.erb` y necesita ser localizado dentro de la carpeta `app/views` de la aplicación.

Ahora ve y crea un nuevo archivo en `app/views/articles/new.html.erb` y escribe el siguiente
contenido en él:

```html
<h1>New Article</h1>
```

Cuando refresques <http://localhost:3000/articles/new>, verás que la página tiene un título. La ruta,
el controlador, la acción y la vista ahora están funcionando de manera armoniosa! Es hora de crear
el formulario para un nuevo post.

El primer formulario
====================

Para crear una formulario con esta plantilla usarás un _constructor de formularios_ (o _form builder_
en inglés). El _form builder_ primario de Rails está provisto por un método de ayuda llamado `form_for`.
Para usar este método agrega este código a `app/views/articles/new.html.erb`:

```html+erb
<%= form_for :article do |f| %>
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

Si actualizas la página, ahora verás el mismo formulario del ejemplo.
¡Construir un formulario en Rails es así de sencillo!

Cuando llamas a `form_for`, le pasas un objeto identificador a este
formulario, que en este caso, es el símbolo `:article`. Esto le indica al método
`form_for` para quién es dicho formulario. Dentro del bloque de este método,
el objeto `FormBuilder` - representado por `f` - es usado para construir dos
etiquetas y dos cajas de texto, sea una para el título y la otra para el texto del
post. Finalmente, la llamada al método `submit` en el objeto `f` creará un
botón de submit en el formulario.

Sin embargo, existe un problema con este formulario. Si inspeccionas el código
HTML generado, al observar el código fuente de la página, verás que el atributo `action` del formulario apunta a `/articles/new`. Esto es un problema debido a que esta ruta
va a la misma página donde te encuentras en este momento, cuando en realidad la
ruta debería sólo ser usada para mostrar el formulario para un nuevo post.

El formulario necesita usar un URL distinto para poder dirigirse hacia algún otro
lugar. Esto puede hacerse, de manera bastante sencilla, con la opción `:url` de
`form_for`. En Rails la acción que se usa típicamente para nuevas entradas es llamada
"_create_" (_crear_ en español) por lo que el formulario debería ser apuntado hacia
esa acción.

Edita la siguiente línea de `form_for`: `app/views/articles/new.html.erb` para que
se vea así:

```html+erb
<%= form_for :article, url: articles_path do |f| %>
```

En este ejemplo se pasa el _helper_ `articles_path` a la opción `:url`. Para comprender qué es lo que hace Rails con este objeto, recuerda cómo era el resultado de ejecutar el comando `rails routes`:

```bash
$ bin/rails routes
      Prefix Verb   URI Pattern                  Controller#Action
    articles GET    /articles(.:format)          articles#index
             POST   /articles(.:format)          articles#create
 new_article GET    /articles/new(.:format)      articles#new
edit_article GET    /articles/:id/edit(.:format) articles#edit
     article GET    /articles/:id(.:format)      articles#show
             PATCH  /articles/:id(.:format)      articles#update
             PUT    /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy
        root GET    /                            welcome#index
```

El _helper_ `articles_path` le dice a Rails que apunte el formulario a la URI asociada con el prefijo `articles`, por lo que el formulario enviará por defecto peticiones POST a esa ruta. Esta ruta está asociada con la acción create del controlador actual, `ArticlesController`.

Con el formulario y su ruta asociada definidas, serás capaz de llenar el formulario y dar clic en el
botón de submit para empezar el proceso de creación de un nuevo post, así que ve y haz eso. Cuando
des clic al botón y envíes el formulario, te encontrarás con un error familiar.

![Unknown action create for PostsController](http://guides.rubyonrails.org/images/getting_started/unknown_action_create_for_articles.png)

Ahora necesitas crear la acción `create` en `ArticleController` para que funcione.

Creando artículos
=================

Para hacer que "Unknown action" desaparezca, puedes definir una acción `create`
dentro de la clase `ArticleController` en `app/controllers/articles_controller.rb`, debajo de la acción `new`:

```ruby
class ArticlesController < ApplicationController
  def new
  end

  def create
  end
end
```
Si reenvias el formulario ahora no veras ningun cambio en la pagina. Esta bien, esto es porque Rails
por defecto devuelve `204 No Content` a una acción si no se especifica cuál debe ser la respuesta.
Añadimos la accion `create` pero no especificamos cual debe ser la respuesta. En este caso, la acción `create` debe salvar el nuevo artículo en la base de datos.

Cuando un formulario es enviado, los campos del formulario son enviados a Rails como _parámetros_. Estos
parámetros pueden ser referenciados dentro de las acciones del controlador, generalmente para realizar una
tarea determinada. Para ver qué hacen estos parámetros, cambiar la acción `create` a esto:

```ruby
def create
  render plain: params[:article].inspect
end
```

El método `render` toma un simple hash con la clave `:plain` y el valor de `params[:post].inspect`. El
método `params` es el objeto que representa a los parámetros (o campos) que vienen desde el formulario.
El método `params` retorna un objeto `ActionController::Parameters`, que te permite acceder a las claves del hash
usando cadenas o símbolos. En esta situación, los únicos parámetros que importan son los que vienen del
formulario.

Si reenvías el formulario una vez más, ya no obtendrás el error de plantilla faltante, en su lugar verás
algo como lo que sigue:

```ruby
<ActionController::Parameters {"title"=>"First Article!", "text"=>"This is my first article."} permitted: false>
```

Esta acción muestra ahora los parámetros para el artículo que están llegando desde el formulario. Sin
embargo, esto no es realmente útil. Sí, puedes ver los parámetros, pero no hay nada en particular que se
está haciendo con ellos.

Creando el modelo Article
======================

Los modelos en Rails usan un nombre en singular, y sus correspondientes tablas
de base de datos usan un nombre en plural. Rails provee un generador para crear
modelos, el cual la mayoría de desarrolladores en Rails tienden a usar para
crear nuevos modelos. Para crear un nuevo modelo, ejecuta este comando en tu
terminal:

```bash
$ rails generate model Article title:string text:text
```

Con ese comando le decimos a Rails que nosotros queremos un modelo `Article`,
junto con un atributo _title_ de tipo _string_, y un atributo _texto_ de tipo
_text_. Esos atributos son automáticamente añadidos a la tabla `articles` en la
base de datos y mapeados al modelo `Article`.

Rails respondió con la creación de un montón de archivos. Por ahora, nosotros
sólo estamos interesados en `app/models/article.rb` y
`db/migrate/20140120191729_create_articles.rb` (en tu caso puede ser un poco
diferente). Este último es responsable de crear la estructura de la base
de datos, que es lo que revisaremos luego.

> **TIP:** Active Record es lo suficientemente inteligente para asignar
automáticamente el nombre de las columnas a atributos del modelo,
lo que significa que tú no tienes que declarar los atributos dentro
de los modelos de Rails, ya que será realizado automáticamente por
Active Record.

Ejecutando una migración
========================

Como hemos visto, `rails generate model` crea un archivo _database
migration_ dentro del directorio `db/migrate`.
Las migraciones son clases de Ruby que están diseñadas para hacer simple la
creación y modificación de las tablas de la base de datos. Rails usa comandos rake
para ejecutar migraciones, y es posible deshacer una migración después de que ha sido aplicada
a la base de datos. Los archivos de migraciones incluyen una marca de la fecha y hora para
que sean procesadas en el orden que fueron creadas.

Si miras dentro del archivo `db/migrate/YYYYMMDDHHMMSS_create_articles.rb` (recuerda,
tu archivo puede tener un nombre ligeramente diferente), esto es lo que encontrarás:

```ruby
class CreateArticles < ActiveRecord::Migration[5.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :text

      t.timestamps
    end
  end
end
```

La migración de arriba crea un método llamado `change` el cual será llamado cuando ejecutes
la migración. La acción definida en este método es reversible, lo cual significa que Rails
conoce cómo deshacer los cambios realizados en esta migración en caso que necesites hacerlo
más tarde. Cuando ejecutas esta migración se creará una tabla `articles` con una columna tipo `string`
y otra columna tipo `text`. También crea dos campos de fecha-hora para permitir a Rails realizar
un seguimiento de las actualizaciones.

Mayor información acerca de las migraciones en Rails
puede ser encontrada en la guía [Rails Database Migrations](http://guides.rubyonrails.org/migrations.html).

En este punto, puedes usar el comando rake para ejecutar la migración:

```bash
$ rails db:migrate
```

Rails ejecutará este comando de migración y te responderá lo siguiente cuando haya
creado la tabla `articles`.

```bash
==  CreateArticles: migrating ==================================================
-- create_table(:articles)
   -> 0.0019s
==  CreateArticles: migrated (0.0020s) =========================================
```

> **Nota:** Debido a que estás trabajando en el ambiente de desarrollo por omisión,
este comando se aplicará a la base de datos definida en la sección `development`
de tu archivo `config/database.yml`. Si deseas ejecutar migraciones en otro
ambiente, por ejemplo en producción, debes indicarlo en forma explícita cuando
invoques el comando: `rails db:migrate RAILS_ENV=production`.

Salvando datos en el controlador
================================

En `ArticlesController` necesitamos cambiar la acción `create` para usar el nuevo modelo `Article`
y guardar los datos en la base de datos. Abre `app/controllers/articles_controller.rb` y cambia la
acción `create` que debe verse de la siguiente manera:

```ruby
def create
  @article = Article.new(params[:article])

  @article.save
  redirect_to @article
end
```

Esto es lo que sucede: cada modelo Rails puede ser inicializado con sus respectivos
atributos, los cuales son automáticamente asignados a sus respectivas columnas de
base de datos. En la primera línea hacemos justamente eso (recuerda que
`params[:article]` contiene los atributos en los cuales estamos interesados). Luego,
`@article.save` es responsable de guardar el modelo en la base de datos. Finalmente,
direccionamos al usuario a la acción `show` que definiremos más tarde.

> **TIP:** Como veremos más tarde, `@article.save` devuelve un indicador que indica si el
modelo fue guardado o no.

Si recargas de nuevo la página http://localhost:3000/articles/new serás casi capaz de crear un nuevo artículo. Si lo pruebas, verás que se muestra este mensaje de error:

![ActiveModel::ForbiddenAttributesError](http://guides.rubyonrails.org/images/getting_started/forbidden_attributes_for_new_article.png)

Rails incluye varias opciones para ayudarte a desarrollar aplicaciones seguras y ahora mismo estás viendo
una de ellas. Esta opción se llama `strong_parameters` y obliga a decirle a Rails exactamente qué parametros estan disponibles en la accion de nuestros controladores.

Porque esto tiene que importarte? La capacidad de tomar y asignar todos los parámetros del controlador para su modelo automáticamente hace el trabajo del programador mas facil, pero por esta comodidad también permite un uso malintencionado. ¿Qué pasa si una solicitud al servidor fue diseñado para parecerse a un nuevo artículo, pero también incluyó campos adicionales con valores que violan la integridad de su aplicación? Serían "asignados en masa" en su modelo y luego en la base de datos junto con los buenos - esto puede potencialmente romper su aplicación, o peor.

Como en este caso sólo nos interesan los atributos `title` y `text`, debes añadir el siguiente método `article_params` y cambiar el código de la acción `create`:

```ruby
def create
  @article = Article.new(article_params)

  @article.save
  redirect_to @article
end

private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

Mostrando artículos
===================

Si envías el formulario de nuevo, Rails se quejará de que no has definido la acción `show`.
Esto no es muy útil así que vamos a agregar la acción `show` antes de continuar.

Como viste en la salida del comando `rails routes`, la ruta de la acción `show` tiene este aspecto:

```bash
article GET    /articles/:id(.:format)      articles#show
```

La sintaxis `:id` de la ruta indica a Rails que esta ruta espera un parámetro llamado `:id`, que en este caso será el atributo id del artículo que se quiere ver.

Como hicimos anteriormente, es necesario añadir una nueva acción en el archivo `app/controllers/articles_controller.rb` y también hay que crear su vista correspondiente.

Vamos a añadir la acción show, de la siguiente manera:

```ruby
class ArticlesController < ApplicationController
  def show
    @article = Article.find(params[:id])
  end

  def new
  end
```
Un par de cosas que debes tener en cuenta: usamos `Article.find` para encontrar el artículo que nos interesa, pasándole el valor `params[:id]` para obtener el parámetro `:id` directamente de la petición. También usamos una variable de instancia (con el prefijo @) para guardar una referencia al objeto del artículo. Hacemos eso porque Rails pasa automáticamente todas las variables de instancia a la vista.

Ahora, crea un nuevo archivo `app/view/articles/show.html.erb` con el siguiente contenido:

Abre el archivo `config/routes.rb` y agrega la siguiente ruta:

```ruby
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
```

Finalmente, si vas a
[http://localhost:3000/posts/new](http://localhost:3000/articles/new) serás capaz de
crear un artículo. ¡Inténtalo!

![Show action for posts](http://guides.rubyonrails.org/images/getting_started/show_action_for_articles.png)

Listando todos los artículos
============================

Aún necesitamos una forma de listar todos los artículos, de manera que vamos a hacerlo.
La ruta que corresponde a esta acción según el comando `rails routes` es:

```bash
articles GET    /articles(.:format)          articles#index
```

Y la acción index para esta ruta dentro de `ActionController` del archivo `app/controllers/articles_controller.rb` debería ser:

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
  end
```
y finalmente, añadir la vista para esta accion, ubicada en `app/views/articles/index.html.erb:`:

```html+erb
<h1>Listing articles</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

Ahora si vamos a `http://localhost:3000/articles` veremos una lista con todos los artículos que has creado.

Agregando enlaces
=================

Hasta el momento puedes crear, mostrar y listar artículos. Ahora vamos a agregar
algunos enlaces para navegar a través de las páginas.

Abre `app/views/welcome/index.html.erb` y modifîcalo como se indica a continuación:

```html+erb
<h1>Hello, Rails!</h1>
<%= link_to 'My Blog', controller: 'articles' %>
```

El método `link_to` es uno de los asistentes de la vista incorporados en Rails.
Este método crea el hipervínculo mostrando un texto e indicando a dónde irá, en
este caso a la ubicación `articles`.

Vamos a agregar enlaces a las otras vistas, empezando por agregar a "New Article"
el enlace a `app/views/articles/index.html.erb`, ubicándola encima de la etiqueta
`<table>`:

```erb
<%= link_to 'New article', new_article_path %>
```

Este enlace te permitirá abrir el formulario para crear un nuevo artículo.

También deberías agregar un enlace a esta plantilla -- `app/views/articles/new.html.erb` --
para regresar a la acción `index`. Para hacer eso agrega el enlace debajo del
formulario en esta plantilla:

```erb
<%= form_for :article, url: articles_path do |f| %>
  ...
<% end %>

<%= link_to 'Back', articles_path %>
```

Finalmente, agrega otro enlace a la plantilla `app/views/articles/show.html.erb` para regresar
a la acción `index`, de manera que la persona que está viendo un artículo pueda regresar
y ver la lista completa nuevamente.

```html+erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>

<%= link_to 'Back', articles_path %>
```

> **TIP:** Si deseas crear un enlace a una acción dentro del mismo controlador
no necesitas especificar la opción `:controller`, Rails usará el actual
controlador por omisión.

> **TIP:** En modo de desarrollo (en la cual estás trabajando por omisión), Rails recarga
los archivos de tu aplicación en cada petición del navegador, por lo que no hay
necesidad de reiniciar el servidor web cuando un cambio es realizado.

Agregando algunas validaciones
======================================

El archivo del modelo `app/models/article.rb` es tan simple como:

```ruby
class Article < ApplicationRecord
end
```

No hay mucho en ese archivo - pero nota que la clase `Article` hereda de
`ApplicationRecord`. `ApplicationRecord` hereda de `ActiveRecord::Base`
provee una gran cantidad de funcionalidad a los modelos de Rails de forma
sencilla, incluyendo las operaciones básicas CRUD (del inglés Create, Read,
Update, Destroy) de base de datos, validación de datos así como el soporte
a búsquedas sofisticadas y la habilidad de relacionar múltiples modelos
entre sí.

Rails incluye métodos que ayudaran a asegurar los campos de tu modelo.
Abre el archivo `app/models/article.rb` y complétalo de esta manera:

```ruby
class Article < ApplicationRecord
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```
Estos cambios asegurarán que todos los artículos tengan un título que sea al
menos de cinco caracteres de longitud. Rails puede validar una variedad de
condiciones en un modelo, incluyendo la presencia o la unicidad de columnas,
sus formatos y la existencia de objetos asociados. Las validaciones están cubiertas
en detalle en [Active Record Validations and Callbacks](http://guides.rubyonrails.org/active_record_validations.html).

Con las validaciones agregadas, cuando llames a `@article.save` en un artículo
inválido
retornará `false`. Si abres el archivo `app/controllers/articles_controller.rb`
otra vez, notarás que no verificamos el resultado de la llamada `@article.save`
dentro de la acción `create`. Si `@article.save` falla en esta situación, necesitamos mostrar
el formulario de regreso al usuario. Para hacer esto, cambiar las acciones `new` y `create`
dentro de `app/controllers/articles_controller.rb` a esto:

```ruby
def new
  @article = Article.new
end

def create
  @article = Article.new(article_params)

  if @article.save
    redirect_to @article
  else
    render 'new'
  end
end

private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

La acción `new` está ahora creando una nueva instancia llamada `@article`,
y verás el motivo de ello en un momento.

Notas que dentro de la acción `create` usamos `render` en lugar de `redirect_to` cuando acción `save`
retorna `false`. El método `render`es usado de manera que el objeto `@article`es regresado a la plantilla
`new` cuando es interpretado. Esta interpretación se hace dentro de la misma solicitud que hace el envío
del formulario, mientras que `redirect_to`le dirá al navegador para emitir una nueva solicitud.

Si recargas [http://localhost:3000/articles/new](http://localhost:3000/articles/new) y
tratas de guardar un artículo sin título, Rails enviará de regreso un formulario
pero que no es muy útil. Necesitas decirle al usuario que algo está mal.
Para hacer esto hay que modificar el archivo `app/views/articles/new.html.erb`
para verificar los mensajes de error:

```html+erb
<%= form_for :article, url: articles_path do |f| %>

  <% if @article.errors.any? %>
    <div id="error_explanation">
      <h2>
        <%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:
      </h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>
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

<%= link_to 'Back', articles_path %>
```

Veamos qué está pasando. Verificamos si hay errores con
`@article.errors.any?` y en caso que los haya mostramos una lista de todos
los errores con `@article.errors.full_messages`.

`pluralize` es un asistente de Rails que toma un número, un texto y sus argumentos.
Si el número es mayor de 1, el texto será automáticamente pluralizado

La razón de por qué agregamos `@article = Article.new` en `ArticlesController`
es que de otra manera `@article` será `nil` en tu vista y llamar a
`@article.errors.any?` mostrará un error.

CONSEJO: Rails automaticamente ajustará los campos que contienen error en un `div`
dentro de la clase `field_with_errors`. Puedes definir una regla `css` para destacarlos.

Ahora verás un bonito mensaje de error cuando intentes guardar un artículo sin título
en [new post form (http://localhost:3000/articles/new)](http://localhost:3000/articles/new).

![Form With Errors](http://guides.rubyonrails.org/images/getting_started/form_with_errors.png)

Actualizando artículos
======================

Hemos cubierto la parte "CR" del acrónimo CRUD. Ahora nos enfocaremos en la
parte "U", actualización de artículos.

El primer paso será agregar la acción `edit` al `ArticlesController`, generalmente
entre las acciones `new` and `create`:


```ruby
def new
  @article = Article.new
end

def edit
  @article = Article.find(params[:id])
end

def create
  @article = Article.new(article_params)

  if @article.save
    redirect_to @article
  else
    render 'new'
  end
end
```

La vista contendrá un formulario similar al que usamos cuando creamos
nuevos artículos. Crea un archivo llamado `app/views/articles/edit.html.erb` que
contenga lo siguiente:

```html+erb
<h1>Editing article</h1>

<%= form_for :article, url: article_path(@article), method: :patch do |f| %>

  <% if @article.errors.any? %>
    <div id="error_explanation">
      <h2>
        <%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:
      </h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>
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

<%= link_to 'Back', articles_path %>
```

Esta vez indicamos al formulario la acción `update`, la cual no está definido aún
pero pronto lo estará.

La opción `method: :patch` le dice a Rails que queremos que este formulario sea
enviado a través del método HTTP `PATCH HTTP`, el cual es el método que tú esperas
que se use para **actualizar** recursos de acuerdo al protocolo REST.

El primer parámetro de form_for puede ser un objeto, por ejemplo `@article`, que
se utiliza para rellenar los campos del formulario. Si pasas un símbolo
(ejemplo `:article`) cuyo nombre sea idéntico al de una variable de instancia
(`@article`) el funcionamiento es el mismo. Esto es precisamente lo que está
pasando en este ejemplo. Consulta la documentación de form_for para conocer más
detalles.

A continuación, crea la acción update en el archivo `app/controllers/articles_controller.rb`.
Agregar esto entre la accion `create` y el metodo `private`:

```ruby
def create
  @article = Article.new(article_params)

  if @article.save
    redirect_to @article
  else
    render 'new'
  end
end

def update
  @article = Article.find(params[:id])

  if @article.update(article_params)
    redirect_to @article
  else
    render 'edit'
  end
end

private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

El nuevo método `update`, es usado cuando deseas actualizar un registro
que ya existe, y acepta un hash conteniendo los atributos que deseas actualizar.
Como hicimos anteriormente, si hay un error actualizando el artículo queremos
mostrar el formulario de regreso al usuario.
Para ello se reutiliza el método `article_params` definido anteriormente para la
acción `create`.

CONSEJO: no necesitas enviar todos los atributos a `update`. Por
ejemplo, si llamas a `@article.update(title: 'A new title')`
Rails solo actualizará el atributo `title` sin tocar los otros atributos.

Finalmente, queremos mostrar un enlace a la acción `edit` en la lista de todos
los artículos, de esta manera hacemos que ahora en `app/views/articles/index.html.erb`
aparezca un nuevo enlace adicional a la acción `show`:

```html+erb
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th colspan="2"></th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
      <td><%= link_to 'Edit', edit_article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

Y también la agregaremos en la plantilla `app/views/articles/show.html.erb` de manera que
haya un enlace "Edit" en la página del artículo. Agregar esto al final de tu plantilla:

```html+erb
...
<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

Y así es cómo nuestra aplicación se ve hasta el momento

![Index action with edit link](http://guides.rubyonrails.org/images/getting_started/index_action_with_edit_link.png)

Usando parciales para eliminar la duplicidad en las vistas
==========================================================

La página `edit` se parece mucho a la página `new` porque utilizan el mismo código
para mostrar el formulario. Así que vamos a eliminar estas duplicidades mediante
los parciales. Por convención un parcial es un archivo de plantilla cuyo nombre
empieza por un guión bajo y cuyo contenido se reutiliza en varias plantillas
diferentes.

CONSEJO: Puedes leer más acerca de parciales en la guía
[Layouts and Rendering in Rails](http://guides.rubyonrails.org/layouts_and_rendering.html).

Crea un nuevo archivo `app/views/articles/_form.html.erb` con el siguiente contenido:

```html+erb
<%= form_for @article do |f| %>
 <% if @article.errors.any? %>
    <div id="error_explanation">
      <h2>
        <%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:
      </h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>
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
Todo este contenido, excepto la declaración form_for, es idéntico al contenido
que ya teníamos. Como `@article` es un recurso que incluye todas las rutas
RESTful y Rails es capaz de inferir qué URI y método se debe utilizar, podemos
simiplificar al máximo la declaración `form_for`. Consulta la guía
[Resource-oriented style](http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html#method-i-form_for-label-Resource-oriented+style)
para obtener más información sobre este uso de `form_for`.

Por ahora, vamos a actualizar la vista `app/views/articles/new.html.erb` para
usar el nuevo parcial, reescribiendo completamente:

```html+erb
<h1>New article</h1>

<%= render 'form' %>

<%= link_to 'Back', articles_path %>
```

Luego hacer lo mismo a la vista `app/views/articles/edit.html.erb`:

```html+erb
<h1>Edit article</h1>

<%= render 'form' %>

<%= link_to 'Back', articles_path %>
```

Eliminando artículos
====================

Ahora estamos listos para cubrir la parte "D" del acrónimo CRUD: eliminar artículos
de la base de datos. Siguiendo la convención REST, vamos a agregar una ruta para la
eliminación de artículos a `bin/rails routes`:

```bash
DELETE /articles/:id(.:format)      articles#destroy
```

El método de enrutamiento `delete` debe ser usado para métodos que destruyen recursos.
Si se deja como un típico comando de ruteo `get`, es posible que se puedan enviar
URLs malintencionadas como estas:

```html
<a href='http://example.com/articles/1/destroy'>look at this cat!</a>
```

Nosotros usamos el método `delete` para destruir recursos y este ruteo está enlazado
con la acción `destroy` dentro de `app/controllers/articles_controller.rb`, la
cual no existe todavia. El metodo `destroy` es generalmente la ultima accion en el
CRUD en el controlador, y como las otras acciones CRUD publicas, debe estar antes
de cualquiera de los metodos privados o protegidos.

```ruby
def destroy
  @article = Article.find(params[:id])
  @article.destroy

  redirect_to articles_path
end
```
El `ArticlesController` completo en `app/controllers/articles_controller.rb` debería
tener este aspecto:

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def edit
    @article = Article.find(params[:id])
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render 'new'
    end
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render 'edit'
    end
  end

  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to articles_path
  end

  private
    def article_params
      params.require(:article).permit(:title, :text)
    end
end
```

Puedes llamar a `destroy` en objetos Active Record cuando desees eliminarlos de la
base de datos. Hay que tener en cuenta que no necesitas agregar una vista para esta acción ya que
estamos siendo redireccionados a la acción `index`.

Finalmente, agregamos un enlace a la plantilla de la acción `index`
(`app/views/articles/index.html.erb`) para completar todo.

```html+erb
<h1>Listing Articles</h1>
<%= link_to 'New article', new_article_path %>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th colspan="3"></th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
      <td><%= link_to 'Edit', edit_article_path(article) %></td>
      <td><%= link_to 'Destroy', article_path(article),
              method: :delete,
              data: { confirm: 'Are you sure?' } %></td>
    </tr>
  <% end %>
</table>
```
En esta plantilla se utiliza `link_to` de una manera diferente. El nombre de la
ruta se pasa como segundo argumento y después se indican las opciones mediante otro
argumento. Las opciones `method: :delete` and `data: { confirm: 'Are you sure?' }`
se utilizan como atributos HTML5 para que cuando se hace click sobre el enlace Rails muestre
un mensaje de confirmación al usuario, y luego enviar el metodo `delete`.

Este comportamiento es posible gracias al archivo JavaScript llamado jquery_ujs, que se incluye automáticamente en el layout de la aplicación (app/views/layouts/application.html.erb) que se creó al generar la aplicación Rails. Si no se incluye este archivo, el mensaje de confirmación no se muestra.

![Confirm Dialog](http://guides.rubyonrails.org/images/getting_started/confirm_dialog.png)

Felicitaciones, ahora puedes crear, mostrar, enumerar, actualizar y eliminar
artículos.

Agregando un Segundo Modelo
===========================

Es hora de agregar un segundo modelo a la aplicación. El segundo modelo debe
manejar los comentarios de los artículos.

Generando un Modelo
===================

Vamos a usar el mismo generador que usamos antes al crear el modelo `Article`. Esta
vez crearemos el modelo `Comment` para los comentarios del artículo. Ejecuta
esto en tu terminal:

```bash
$ rails generate model Comment commenter:string body:text article:references
```

Este comando generará cuatro archivos:

| Archivo                                      | Propósito                                                                                                |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------|
| db/migrate/20140120201010_create_comments.rb | Migración para crear la tabla de comentarios en tu base de datos |
| app/models/comment.rb                        | El modelo Comment.                                                                                       |
| test/models/comment_test.rb                  | Pruebas unitarias para el modelo de comentarios.                                                         |
| test/fixtures/comments.yml                   | Muestras de comentarios para usar de pruebas.                                                            |

Primero, miremos `app/models/comment.rb`:

```ruby
class Comment < ApplicationRecord
  belongs_to :article
end
```

Ésto es muy similar al modelo `Article` que vimos antes. La diferencia es la
línea `belongs_to :article`, que establece una asociación de Active Record.
Aprenderás un poco más sobre asociaciones en la siguiente sección de esta
guía.

La palabra clave (`:references`) utilizada en el comando bash es un tipo estacial
de datos para los modelos. Se crea una nueva columna en la tabla de base de datos
con el nombre del modelo proporcionado con un `_id` que puede contener valores
enteros. Se puede obtener una mejor comprensión después de analizar el archivo
`db/schema.rb` a continuación.

Además del modelo, Rails hizo la migración para crear la tabla correspondiente
en la base de datos:

```ruby
class CreateComments < ActiveRecord::Migration[5.0]
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :article, foreign_key: true

      t.timestamps
    end
  end
end
```
La línea de `t.references` crea una columna entera llamada `article_id`, un índice,
y una restricción de `foreign key` que apunta a la columna id de la tabla `articles`.
Corre la migración:

```bash
$ rails db:migrate
```

Rails es suficientemente listo para sólo ejecutar las migraciones que no se han
ejecutado todavía en la base de datos actual, así que en este caso sólo verás:

```bash
==  CreateComments: migrating =================================================
-- create_table(:comments)
   -> 0.0115s
==  CreateComments: migrated (0.0119s) ========================================
```

Asociando Modelos
=================

Las asociaciones de Active Record te permiten declarar fácilmente la relación
entre dos modelos. En el caso de los comentarios y artículos, puedes escribir la
relación de esta manera:

* Cada comentario pertence a un artículo.
* Un artículo puede tener muchos comentarios.

De hecho, ésto es muy cercano a la sintáxis que usa Rails para declarar esta
asociación. Ya has visto la línea de código en el modelo `Comment (app/models/comment.rb)`  
que hace que cada comentario pertenezca a un artículo:

```ruby
class Comment < ApplicationRecord
  belongs_to :article
end
```

Vas a tener que editar el archivo `app/models/article.rb` para agregar el otro
lado de la asociación:

```ruby
class Article < ApplicationRecord
  has_many :comments
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```

Estas dos declaraciones permiten bastante comportamiento automatizado. Por
ejemplo, si tienes una variable de instancia `@article` conteniendo un artículo,
puedes obtener todos los comentarios que pertenecen a ese artículo como un
arreglo usando `@article.comments`.

SUGERENCIA: Para más información sobre las asociaciones de Active Record, revisa
la guía [Active Record Associations](http://guides.rubyonrails.org/association_basics.html)
(en inglés).

Agregando una Ruta para Comentarios
===================================

Así como con el controlador `welcome`, vamos a necesitar agregar una ruta para
que Rails sepa donde queremos navegar para ver `comments`. Abre el archivo
`config/routes.rb`, y edítalo de la siguiente manera:

```ruby
resources :articles do
  resources :comments
end
```

Esta configuración crea la ruta `comments` dentro de la ruta `articles` que definimos
anteriormente. Esta es otra forma de establecer la relación entre los dos modelos.

SUGERENCIA: Para más información sobre el ruteo, mira la guía
[Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html)
(en inglés).

Generando un Controlador
========================

Con el modelo terminado, necesitamos crearle un controlador. Nuevamente,
usaremos el mismo generador que antes:

```bash
$ rails generate controller Comments
```

Esto crea seis diferentes archivos y una carpeta vacía:

| Archivo/Carpeta                              | Propósito                                   |
| -------------------------------------------  | --------------------------------------------|
| app/controllers/comments_controller.rb       | El controlador de Comments.                 |
| app/views/comments/                          | Donde se guardan las vistas del controlador.|
| test/controllers/comments_controller_test.rb | Las pruebas funcionales del controlador.    |
| app/helpers/comments_helper.rb               | El helper de la vista.                      |
| app/assets/javascripts/comment.coffee        | CoffeeScript para el controlador.           |
| app/assets/stylesheets/comment.scss          | Hojas de estilo para el controlador.        |

Como con cualquier blog, nuestros lectores crearán sus comentarios directamente
después de leer el artículo, y una vez que agregaron su comentario, serán
enviados de vuelta al artículo para ver su comentario ahora listado. Debido a
esto, nuestro `CommentsController` está ahí para proveer un método para crear
comentarios y eliminar spam cuando aparezca.

Así que en primer lugar vamos a modificar la plantilla que muestra los artículos
(`app/views/articles/show.html.erb`) para que deje crear nuevos comentarios:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>

<h2>Add a comment:</h2>
<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

Ésto agrega un formulario en la vista `show` del artículo que crea un
comentario al llamar a la acción `create` en el `CommentsController`. Al llamar
`form_for` se necesita pasar un arreglo, que construirá una ruta anidada,
siguiendo el esquema `/articles/1/comments`.

El siguiente paso consiste en crear la acción create en `app/controllers/comments_controller.rb`:

```ruby
class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end

  private
    def comment_params
      params.require(:comment).permit(:commenter, :body)
    end
end
```

Verás un poco más de complejidad aquí comparado a lo visto en el controlador de
artículos. Eso es un efecto secundario del anidado que estás usando. Cada vez
que se crea un comentario es necesario saber a que artículo pertenece. Por eso
la primera llamada al método `find` del modelo `Article`, para ubicar el artículo
en particular.

Además, el código trata de tomar ventaja de algunos de los métodos disponibles
a las asociaciones. Usamos el método `create` en `@article.comments` para crear y
guardar el comentario. Esto asociará automaticamente el comentario el artículo
en particular.

Una vez que hemos hecho el comentario nuevo, enviamos al usuario de vuelta al
artículo original usando el helper `article_path(@article)`. Como hemos podido ver,
ésto luego llama a la acción `show` en el `ArticlesController` que hace render con
la plantilla `show.html.erb`. Aquí es donde queremos mostrar los comentarios,
así que agreguemos `app/views/posts/articles.html.erb`.

```html+erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>

<h2>Comments</h2>
<% @article.comments.each do |comment| %>
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
<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

Ahora puedes agregar artículos y comentarios a tu blog, y hacer que se muestren
en los lugares correctos.

![Artículo con Comentarios](http://guides.rubyonrails.org/images/getting_started/article_with_comments.png)

Haciendo Refactoring
====================

Ahora que tenemos los artículos y comentarios funcionando, dale una mirada a la
plantilla `app/views/articles/show.html.erb`. Se está volviendo larga y complicada.
Podemos usar parciales (_partials_) para simplificarla.

Renderizando colecciones de parciales
-------------------------------------

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

Luego puedes cambiar `app/views/articles/show.html.erb` para que se vea de esta
manera:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>

<h2>Comments</h2>
<%= render @article.comments %>

<h2>Add a comment:</h2>
<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

Ésto hará que el parcial en `app/views/comments/_comment.html.erb` se haga
render una vez por cada comentario en la colección `@article.comments`.
A medida que el método `render` itera sobre la colección `@article.comments`,
asigna cada comentario a la variable local llamada igual que el parcial, en este caso
`comment` que luego está disponible en el parcial para que la usemos.

Renderizando un formulario parcial
=====================

Movamos también la sección de comentarios nuevos a su propio parcial. De nuevo,
crea un archivo `app/views/comments/_form.html.erb` que contenga:

```html+erb
<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

Luego haz que `app/views/articles/show.html.erb` se vea de la siguiente manera:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>

<h2>Comments</h2>
<%= render @article.comments %>

<h2>Add a comment:</h2>
<%= render 'comments/form' %>

<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>

```

El segundo render sólo define la plantilla parcial que queremos usar,
`comments/form`. Rails es suficientemente inteligente para detectar el slash en
el texto y darse cuenta que lo que quieres es hacer render del archivo
`_form.html.erb` en la carpeta `app/views/comments`.

El objeto `@article` está disponible a cualquier parcial al que se le haga render
en la vista porque lo hemos definido como una variable de instancia.

Eliminando Comentarios
----------------------

Otra funcionalidad importante para un blog es poder eliminar comentarios spam.
Para hacer esto, necesitamos implementar un enlace de algún tipo en la vista, y
una acción `destroy` en el `CommentsController`.

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
  <%= link_to 'Eliminar Comentario', [comment.article, comment],
               method: :delete,
               data: { confirm: 'Are you sure?' } %>
</p>
```

Al hacer click en este nuevo enlace "Eliminar Comentario" se enviará un `DELETE
/articles/:article_id/comments/:id` a nuestro `CommentsController`, que puede luego usar
para ubicar el comentario que queremos eliminar, así que agreguemos una acción
de eliminar a nuestro controlador (`app/controllers/comments_controller.rb`):

```ruby
class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end

  def destroy
    @article = Article.find(params[:article_id])
    @comment = @article.comments.find(params[:id])
    @comment.destroy
    redirect_to article_path(@article)
  end

  private
    def comment_params
      params.require(:comment).permit(:commenter, :body)
    end
end
```

La acción `destroy` encontrará el artículo que estamos viendo, luego el
comentario en la colección `@article.comments`, para eliminarlo de la base de datos
y enviarnos de vuelta a la acción `show` para el artículo.

Eliminando Objetos Asociados
============================

Si borras un artículo, todos sus comentarios también derían borrarse para que no
ocupen un espacio innecesario en la base de datos. Rails permite configurar este
comportamiento mediante la opción `dependent` de la asociación entre modelos.
Para ello, modifica el modelo `Article` cambiando el contenido del archivo
`app/models/article.rb` por lo siguiente:

```ruby
class Article < ApplicationRecord
  has_many :comments, dependent: :destroy
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```

Seguridad
=========

Si fueras a publicar tu blog en línea, cualquier persona podría agregar, editar
y eliminar artículos o eliminar comentarios.

Rails provee un sistema muy simple de autenticación por HTTP que funcionaría muy
bien en esta situación.

Necesitamos una forma de bloquear el acceso a ciertas acciones en el controlador
`ArticlesController` si la persona no está autenticada, aquí podemos usar el método
de Rails `http_basic_authenticate_with`, que permite acceso a la acción
solicitada si el método retorna `true`.

Para usar el sistema de autenticación, lo especificamos en la parte inicial de
`ArticlesController`, en este caso, queremos autenticar al usuario en cada una de
las acciones, excepto `index` y `show`, así lo escribimos:

```ruby
class ArticlesController < ApplicationController

  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]

  def index
    @articles = Article.all
  end
# cortado por brevedad
```

También queremos limitar la eliminación de comentarios a los usuarios autenticados, así
que en `CommentsController` (`app/controllers/comments_controller.rb`) escribimos:

```ruby
class CommentsController < ApplicationController

  http_basic_authenticate_with name: "dhh", password: "secret", only: :destroy

  def create
    @article = Article.find(params[:article_id])
    # ...
  end
# cortado por brevedad
```

Ahora si intentas crear un nuevo artículo, vas a ser recibido con una ventana
de diálogo de autenticación HTTP básica.

![Ventana de diálogo de autenticación HTTP básica](http://guides.rubyonrails.org/images/getting_started/challenge.png)

Hay otros metodos de autentificacion disponibles para aplicaciones Rails.
Dos de los mas gemas mas populares para Rails son Devise y Authlogic, junto con muchas mas.

Otros comentarios sobre la seguridad
------------------------------------

La seguridad, sobre todo cuando habamos de aplicaciones web, es un tema muy complejo.
Por eso puedes consultar la guía [Ruby on Rails Security Guide](http://guides.rubyonrails.org/security.html) para obtener más información al respecto.

¿Qué sigue?
===========

Ahora que has visto tu primera aplicación en Rails, deberías sentir la libertad
de actualizarla y experimentar por tu cuenta. Pero no necesitas hacer todo sin
ayuda. A medida que vayas necesitando ayuda mientras comienzas con Rails, puedes
consultar estos recursos:

**Inglés**

* El [Agile Web Development with Rails](http://pragprog.com/book/rails4/agile-web-development-with-rails)
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
