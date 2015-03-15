Actualizando artículos
======================

Hemos cubierto la parte "CR" del acrónimo CRUD. Ahora nos enfocaremos en la
parte "U", actualización de artículos.

El primer paso será agregar la acción `edit` al `posts_controller`.

Empecemos agregando una ruta a `config/routes.rb`:

```ruby
get "posts/:id/edit" => "posts#edit"
```

Y luego agregar la acción al controlador:

```ruby
def edit
  @post = Post.find(params[:id])
end
```

La vista contendrá un formulario similar al que usamos cuando creamos
nuevos artículos. Crea un archivo llamado `app/views/posts/edit.html.erb` que contenga
lo siguiente:

```html+erb
<h1>Editing post</h1>

<%= form_for :post, :url => { :action => :update, :id => @post.id },
:method => :put do |f| %>
  <% if @post.errors.any? %>
  <div id="errorExplanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
    <% @post.errors.full_messages.each do |msg| %>
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

<%= link_to 'Back', :action => :index %>
```

Esta vez indicamos al formulario la acción `update`, la cual no está definido aún
pero pronto lo estará.

La opción `:method => :put` le dice a Rails que queremos que este formulario sea enviado
a través del método HTTP `PUT`, el cual es el método que tú esperas que se use para
**actualizar** recursos de acuerdo al protocolo REST.

CONSEJO: Por omisión, los formularios construidos con el asistente `+form_for_` son enviados
a través de `POST`.

A continuación, necesitamos agregar la acción `update`. El archivo
`config/routes.rb` necesitará una línea más:

```ruby
put "posts/:id" => "posts#update"
```

Y luego crear la acción `update` en `app/controllers/posts_controller.rb`:

```ruby
def update
  @post = Post.find(params[:id])

  if @post.update_attributes(params[:post])
    redirect_to :action => :show, :id => @post.id
  else
    render 'edit'
  end
end
```

El nuevo método `update_attributes`, es usado cuando deseas actualizar un registro
que ya existe, y acepta un hash conteniendo los atributos que deseas actualizar.
Como hicimos anteriormente, si hay un error actualizando el artículo, queremos
mostrar el formulario de regreso al usuario.

CONSEJO: no necesitas enviar todos los atributos a `update_attributes`. Por
ejemplo, si llamas a `@post.update_attributes(:title => 'A new title')`
Rails solo actualizará el atributo `title` sin tocar los otros atributos.

Finalmente, queremos mostrar un enlace a la acción `edit` en la lista de todos
los artículos, de esta manera hacemos que ahora en `app/views/posts/index.html.erb`
aparezca un nuevo enlace adicional a la acción `show`:

```html+erb
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
    <th></th>
  </tr>

<% @posts.each do |post| %>
  <tr>
    <td><%= post.title %></td>
    <td><%= post.text %></td>
    <td><%= link_to 'Show', :action => :show, :id => post.id %></td>
    <td><%= link_to 'Edit', :action => :edit, :id => post.id %></td>
  </tr>
<% end %>
</table>
```

Y también la agregaremos en la plantilla `app/views/posts/show.html.erb` de manera que
haya un enlace "Edit" en la página del artículo. Agregar esto al final de tu plantilla:

```html+erb
...

<%= link_to 'Back', :action => :index %>
| <%= link_to 'Edit', :action => :edit, :id => @post.id %>
```

Y así es cómo nuestra aplicación se ve hasta el momento.

![Index action with edit link](http://edgeguides.rubyonrails.org/images/getting_started/index_action_with_edit_link.png)
