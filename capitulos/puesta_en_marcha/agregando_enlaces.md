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
