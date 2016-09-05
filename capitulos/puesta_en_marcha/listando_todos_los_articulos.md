Listando todos los artículos
============================

Aún necesitamos una forma de listar todos los artículos, de manera que vamos a hacerlo.
La ruta que corresponde a esta acción según el comando `rails routes` es:

```bash
articles GET    /articles(.:format)          articles#index
```

Y la acción index para esta ruta dentro de `ActionController` del archivo `app/controllers/articles_controller.rb` debería ser:

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
  end
```
y finalmente, añadir la vista para esta accion, ubicada en `app/views/articles/index.html.erb:`:

```html+erb
<h1>Listing articles</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

Ahora si vamos a `http://localhost:3000/articles` veremos una lista con todos los artículos que has creado.
