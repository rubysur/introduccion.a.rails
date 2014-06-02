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
con un DSL especial (domain-specific language) que le dicen a Rails cómo conectar
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

> **NOTA:** Para mayor información acerca del enrutamiento, ir a
[Rails Routing from the Outside In](http://edgeguides.rubyonrails.org/routing.html).
