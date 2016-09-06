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
