Generando un Controlador
========================

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
enviados de vuelta al artículo para ver su comentario ahora alistado. Debido a
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

Ésto agrega un formulario en la vista `show` del artículo que crea un
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
guardar el comentario. Esto asociará automáticamente el comentario del artículo
en particular.

Una vez que hemos hecho el nuevo comentario , enviamos al usuario de vuelta al
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
en los lugares correctos.

![Artículo con Comentarios](http://edgeguides.rubyonrails.org/images/getting_started/post_with_comments.png)

Haciendo Refactoring
--------------------

Ahora que tenemos los artículos y comentarios funcionando, dale una mirada a la
plantilla `app/views/posts/show.html.erb`. Se está volviendo larga y complicada.
Podemos usar parciales (_partials_) para simplificarla.
