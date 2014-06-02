Usando parciales para eliminar la duplicidad en las vistas
==========================================================

`partials` son lo que Rails usa para remover la duplicidad en las vistas. Aquí hay
un ejemplo:

```html+erb
# app/views/user/show.html.erb

<h1><%= @user.name %></h1>

<%= render 'user_details' %>

# app/views/user/_user_details.html.erb

<%= @user.location %>

<%= @user.about_me %>
```

La plantilla `users/show` automáticamente incluirá el contenido de la plantilla
`users/_user_details`. Nota que los parciales tienen como prefijo un subrayado,
de manera de no confundirlas con vistas regulares. Sin embargo, no incluyas
el subrayado cuando las incluyas dentro del método `helper`.

CONSEJO: Puedes leer más acerca de parciales en la guía
[Layouts and Rendering in Rails](layouts_and_rendering.html).

Nuestra acción `edit` parece muy similar a la acción `new`, en efecto ellos
comparten el mismo código para mostrar el formulario. Vamos a limpiarlo
usando un parcial.

Crea un nuevo archivo `app/views/posts/_form.html.erb` con el siguiente contenido:

```html+erb
<%= form_for @post do |f| %>
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
```

Todo, excepto la declaración `form_for` permanece igual. Como `form_for`
puede averiguar la `action` y los atributos del `method` correcto
cuando construye el formulario será explicado en unos momentos.
Por ahora, vamos a actualizar la vista
`app/views/posts/new.html.erb` para usar el nuevo parcial, reescribiendo completamente:

```html+erb
<h1>New post</h1>

<%= render 'form' %>

<%= link_to 'Back', :action => :index %>
```

Luego hacer lo mismo a la vista `app/views/posts/edit.html.erb`:

```html+erb
<h1>Edit post</h1>

<%= render 'form' %>

<%= link_to 'Back', :action => :index %>
```

Ve con tu navegador a [http://localhost:3000/posts/new](http://localhost:3000/posts/new) y
trata de crear un nuevo artículo. Todo funciona todavía, ahora tratemos de editar el
artículo y recibiremos el siguiente mensaje de error:

![Undefined method post_path](http://edgeguides.rubyonrails.org/images/getting_started/undefined_method_post_path.png)

Para entender este error necesitamos conocer cómo funciona `form_for`.
Cuando pasas un objeto a `form_for` y no especificas la opción de `:url`,
Rails trata de adivinar las opciones de `action` y `method` verificando
si el objeto pasado es un nuevo registro o no. Rails sigue la convención
REST, de esta manera si se está creando un nuevo objeto `Post` buscará por una
ruta llamada `post_path` y para actualizar un objeto `Post` buscará por una
ruta llamada `post_path` y le pasará el objeto actual. Similarmente, Rails conoce
que debe crear nuevos objetos a través de POST y actualizarlos a través de PUT.

Si ejecutas `rake routes` desde la consola verás que ya tenemos una ruta
`posts_path`, la cual fue creada automáticamente por Rails cuando se definió la ruta
por la acción `index`. Sin embargo, no tenemos aún un `post_path`, la cual es la
razón por la que recibimos el error anterior.

```bash
# rake routes

    posts GET  /posts(.:format)            posts#index
posts_new GET  /posts/new(.:format)        posts#new
          POST /posts(.:format)            posts#create
          GET  /posts/:id(.:format)        posts#show
          GET  /posts/:id/edit(.:format)   posts#edit
          PUT  /posts/:id(.:format)        posts#update
     root      /                           welcome#index
```

Para arreglar eso, abrimos el archivo `config/routes.rb` y modificamos la línea `get "posts/:id"`
a esto:

```ruby
get "posts/:id" => "posts#show", :as => :post
```

La opción `:as` le dice al método `get` que queremos hacer que los asistentes
de ruteo llamados `post_url` y `post_path` estén disponibles para nuestra aplicación.
Estos son los métodos que `form_for` necesita cuando estamos editando un artículo y que ahora
están disponibles para actualizar los artículos.

NOTA: La opción `:as` esta disponible también en los métodos de ruteo
`post`, `put`, `delete` y `match`.
