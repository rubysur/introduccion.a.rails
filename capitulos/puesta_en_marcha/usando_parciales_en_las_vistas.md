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
