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
