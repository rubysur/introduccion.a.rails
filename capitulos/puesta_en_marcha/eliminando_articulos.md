Eliminando artículos
====================

Ahora estamos listos para cubrir la parte "D" del acrónimo CRUD: eliminar artículos
de la base de datos. Siguiendo la convención REST, vamos a agregar una ruta para la
eliminación de artículos a `bin/rails routes`:

```bash
DELETE /articles/:id(.:format)      articles#destroy
```

El método de enrutamiento `delete` debe ser usado para métodos que destruyen recursos.
Si se deja como un típico comando de ruteo `get`, es posible que se puedan enviar
URLs malintencionadas como estas:

```html
<a href='http://example.com/articles/1/destroy'>look at this cat!</a>
```

Nosotros usamos el método `delete` para destruir recursos y este ruteo está enlazado
con la acción `destroy` dentro de `app/controllers/articles_controller.rb`, la
cual no existe todavia. El metodo `destroy` es generalmente la ultima accion en el
CRUD en el controlador, y como las otras acciones CRUD publicas, debe estar antes
de cualquiera de los metodos privados o protegidos.

```ruby
def destroy
  @article = Article.find(params[:id])
  @article.destroy

  redirect_to articles_path
end
```
El `ArticlesController` completo en `app/controllers/articles_controller.rb` debería
tener este aspecto:

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def edit
    @article = Article.find(params[:id])
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render 'new'
    end
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render 'edit'
    end
  end

  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to articles_path
  end

  private
    def article_params
      params.require(:article).permit(:title, :text)
    end
end
```

Puedes llamar a `destroy` en objetos Active Record cuando desees eliminarlos de la
base de datos. Hay que tener en cuenta que no necesitas agregar una vista para esta acción ya que
estamos siendo redireccionados a la acción `index`.

Finalmente, agregamos un enlace a la plantilla de la acción `index`
(`app/views/articles/index.html.erb`) para completar todo.

```html+erb
<h1>Listing Articles</h1>
<%= link_to 'New article', new_article_path %>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th colspan="3"></th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
      <td><%= link_to 'Edit', edit_article_path(article) %></td>
      <td><%= link_to 'Destroy', article_path(article),
              method: :delete,
              data: { confirm: 'Are you sure?' } %></td>
    </tr>
  <% end %>
</table>
```
En esta plantilla se utiliza `link_to` de una manera diferente. El nombre de la
ruta se pasa como segundo argumento y después se indican las opciones mediante otro
argumento. Las opciones `method: :delete` and `data: { confirm: 'Are you sure?' }`
se utilizan como atributos HTML5 para que cuando se hace click sobre el enlace Rails muestre
un mensaje de confirmación al usuario, y luego enviar el metodo `delete`.

Este comportamiento es posible gracias al archivo JavaScript llamado jquery_ujs, que se incluye automáticamente en el layout de la aplicación (app/views/layouts/application.html.erb) que se creó al generar la aplicación Rails. Si no se incluye este archivo, el mensaje de confirmación no se muestra.

![Confirm Dialog](http://guides.rubyonrails.org/images/getting_started/confirm_dialog.png)

Felicitaciones, ahora puedes crear, mostrar, enumerar, actualizar y eliminar
artículos.
