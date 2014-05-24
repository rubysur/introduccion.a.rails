Agregando enlaces
=================

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

> **TIP:** Si deseas crear un enlace a una acción dentro del mismo controlador
no necesitas especificar la opción `:controller`, Rails usará el actual
controlador por omisión.

> **TIP:** En modo de desarrollo (en la cual estás trabajdo por omisión), Rails recarga
tu aplicación en cada requerimiento del navegador, por lo que no hay necesidad de
reiniciar el servidor web cuando un cambio es realizado.
