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
