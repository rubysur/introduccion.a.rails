Actualizando artículos
======================

Hemos cubierto la parte "CR" del acrónimo CRUD. Ahora nos enfocaremos en la
parte "U", actualización de artículos.

El primer paso será agregar la acción `edit` al `ArticlesController`, generalmente
entre las acciones `new` and `create`:


```ruby
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
```

La vista contendrá un formulario similar al que usamos cuando creamos
nuevos artículos. Crea un archivo llamado `app/views/articles/edit.html.erb` que
contenga lo siguiente:

```html+erb
<h1>Editing article</h1>

<%= form_for :article, url: article_path(@article), method: :patch do |f| %>

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

<%= link_to 'Back', articles_path %>
```

Esta vez indicamos al formulario la acción `update`, la cual no está definido aún
pero pronto lo estará.

La opción `method: :patch` le dice a Rails que queremos que este formulario sea
enviado a través del método HTTP `PATCH HTTP`, el cual es el método que tú esperas
que se use para **actualizar** recursos de acuerdo al protocolo REST.

El primer parámetro de form_for puede ser un objeto, por ejemplo `@article`, que
se utiliza para rellenar los campos del formulario. Si pasas un símbolo
(ejemplo `:article`) cuyo nombre sea idéntico al de una variable de instancia
(`@article`) el funcionamiento es el mismo. Esto es precisamente lo que está
pasando en este ejemplo. Consulta la documentación de form_for para conocer más
detalles.

A continuación, crea la acción update en el archivo `app/controllers/articles_controller.rb`.
Agregar esto entre la accion `create` y el metodo `private`:

```ruby
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

private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

El nuevo método `update`, es usado cuando deseas actualizar un registro
que ya existe, y acepta un hash conteniendo los atributos que deseas actualizar.
Como hicimos anteriormente, si hay un error actualizando el artículo queremos
mostrar el formulario de regreso al usuario.
Para ello se reutiliza el método `article_params` definido anteriormente para la
acción `create`.

CONSEJO: no necesitas enviar todos los atributos a `update`. Por
ejemplo, si llamas a `@article.update(title: 'A new title')`
Rails solo actualizará el atributo `title` sin tocar los otros atributos.

Finalmente, queremos mostrar un enlace a la acción `edit` en la lista de todos
los artículos, de esta manera hacemos que ahora en `app/views/articles/index.html.erb`
aparezca un nuevo enlace adicional a la acción `show`:

```html+erb
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th colspan="2"></th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
      <td><%= link_to 'Edit', edit_article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

Y también la agregaremos en la plantilla `app/views/articles/show.html.erb` de manera que
haya un enlace "Edit" en la página del artículo. Agregar esto al final de tu plantilla:

```html+erb
...
<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

Y así es cómo nuestra aplicación se ve hasta el momento

![Index action with edit link](http://guides.rubyonrails.org/images/getting_started/index_action_with_edit_link.png)
