Listando todos los artículos
============================

Aún necesitamos una forma de listar todos los artículos, de manera que vamos a hacerlo.
Como de costumbre, vamos a necesitar una ruta ubicada dentro de `config/routes.rb`:

```ruby
get "posts" => "posts#index"
```

Y una acción para esa ruta dentro de `PostsController` en el archivo `app/controllers/posts_controller.rb`:

```ruby
def index
  @posts = Post.all
end
```

Y finalmente una vista para esta acción, ubicada en `app/views/posts/index.html.erb`:

```html+erb
<h1>Listing posts</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>

  <% @posts.each do |post| %>
    <tr>
      <td><%= post.title %></td>
      <td><%= post.text %></td>
    </tr>
  <% end %>
</table>
```

Ahora si vamos a `http://localhost:3000/posts` veremos una lista con todos los artículos que has creado.
