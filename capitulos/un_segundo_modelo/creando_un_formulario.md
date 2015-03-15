Creando un formulario
=====================

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
/posts/:id/comments/:id` a nuestro `CommentsController`, que puede luego usarse
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
