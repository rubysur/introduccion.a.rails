Agregando validaciones
======================

Rails incluye métodos para ayudarte a validar los datos que son enviados a los modelos.
Abre el archivo `app/models/post.rb` y editalo de la siguiente manera:

```ruby
class Post < ActiveRecord::Base
  attr_accessible :text, :title

  validates :title, :presence => true,
                    :length => { :minimum => 5 }
end
```

Estos cambios asegurarán que todos los artículos tengan un título que sea al menos de cinco caracteres
de longitud. Rails puede validar una variedad de condiciones en un modelo, incluyendo la presencia o
la unicidad de columnas, sus formatos y la existencia de objetos asociados. Las validaciones están cubiertas
en detalle en [Active Record Validations and Callbacks](http://edgeguides.rubyonrails.org/active_record_validations_callbacks.html).

Con la validaciones agregadas, cuando llames a `@post.save` en un artículo inválido
retornará `false`. Si abres el archivo `app/controllers/posts_controller.rb`
otra vez, notarás que no verificamos el resultado de la llamada `@post.save`
dentro de la acción `create`. Si `@post.save` falla en esta situación, necesitamos mostrar
el formulario de regreso al usuario. Para hacer esto, cambiar las acciones `new` y `create`
dentro de `app/controllers/posts_controller.rb` a esto:

```ruby
def new
  @post = Post.new
end

def create
  @post = Post.new(params[:post])

  if @post.save
    redirect_to :action => :show, :id => @post.id
  else
    render 'new'
  end
end
```

La acción `new` está ahora creando una nueva instancia llamada `@post`,
y verás el motivo de ello en un momento.

Notas que dentro de la acción `create` usamos `render`en lugar de `redirect_to` cuando acción `save`
retorna `false`. El método `render`es usado de manera que el objeto `@post`es regresado a la plantilla
`new` cuando es interpretado. Esta interpretación se hace dentro de la misma solicitud que hace el envío
del formulario, mientras que `redirect_to`le dirá al navegador para emitir una nueva solicitud.

Si recargas [http://localhost:3000/posts/new](http://localhost:3000/posts/new) y
tratas de guardar un artículo sin título, Rails enviará de regreso un formulario
pero que no es muy útil. Necesitas decirle al usuario que algo está mal.
Para hacer esto hay que modificar el archivo`app/views/posts/new.html.erb`
para verificar los mensajes de error:

```html+erb
<%= form_for :post, :url => { :action => :create } do |f| %>
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

Veamos que está pasando. Verificamos si hay errores con
`@post.errors.any?` y en caso que los haya mostramos una lista de todos
los errores con `@post.errors.full_messages`.

`pluralize` es un asistente de Rails que toma un número, un texto y sus argumentos.
Si el número es mayor de 1, el texto será automáticamente pluralizado

La razón de porque agregamos`@post = Post.new` en `posts_controller` es que de otra
manera `@post` será `nil` en tu vista y llamar a
`@post.errors.any?` mostrará un error.

CONSEJO: Rails automaticamente ajustará los campos que contienen error en un `div`
dentro de la clase `field_with_errors`. Puedes definir una regla `css`para destacarlos.

Ahora enviarás un bonito mensaje de error cuando intentes guardar un artículo sin título
en [new post form (http://localhost:3000/posts/new)](http://localhost:3000/posts/new).

![Form With Errors](http://edgeguides.rubyonrails.org/images/getting_started/form_with_errors.png)
