El primer formulario
====================

Para crear una formulario con esta plantilla usarás un _constructor de formularios_ (o _form builder_
en inglés). El _form builder_ primario de Rails está provisto por un método de ayuda llamado `form_for`.
Para usar este método agrega este código a `app/views/posts/new.html.erb`:

```html+erb
<%= form_for :post do |f| %>
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

Si actualizas la página, ahora verás el mismo formulario del ejemplo.
¡Construir un formulario en Rails es así de sencillo!

Cuando llamas a `form_for`, le pasas un objeto identificador a este
formulario, que en este caso, es el símbolo `:post`. Esto le indica al método
`form_for` para quién es dicho formulario. Dentro del bloque de este método,
el objeto `FormBuilder` - representado por `f` - es usado para construir dos
etiquetas y dos cajas de texto, sea una para el título y la otra para el texto del
post. Finalmente, la llamada al método `submit` en el objeto `f` creará un
botón de submit en el formulario.

Sin embargo, existe un problema con este formulario. Si inspeccionas el código
HTML generado, al observar el código fuente de la página, verás que el atributo `action` del formulario apunta a `/posts/new`. Esto es un problema debido a que esta ruta
va a la misma página donde te encuentras en este momento, cuando en realidad la
ruta debería sólo ser usada para mostrar el formulario para un nuevo post.

El formulario necesita usar un URL distinto para poder dirigirse hacia algún otro
lugar. Esto puede hacerse, de manera bastante sencilla, con la opción `:url` de
`form_for`. En Rails la acción que se usa típicamente para nuevas entradas es llamada
"_create_" (_crear_ en español) por lo que el formulario debería ser apuntado hacia
esa acción.

Edita la siguiente línea de `form_for`: `app/views/posts/new.html.erb` para que
se vea así:

```html+erb
<%= form_for :post, :url => { :action => :create } do |f| %>
```

En este ejemplo, un objeto `Hash` es pasado a la opción `:url`. Lo que Rails hará con
esto es apuntar el formulario a la acción `create` del controlador actual, el `PostsController`.
y enviará una petición de `POST` hacia esa ruta. Para que esto funcione necesitarás añadir
una ruta a `config/routes.rb`, justo debajo de la de "post/new":

```ruby
post "posts" => "posts#create"
```

Al usar el método `post` en vez de `get`, Rails definirá una ruta que solo responderá a métodos POST.
El método POST es el método típico utilizado por todos los formularios a lo largo de la red.

Con el formulario y su ruta asociada definidas, serás capaz de llenar el formulario y dar clic en el
botón de submit para empezar el proceso de creación de un nuevo post, así que ve y haz eso. Cuando
des clic al botón y envíes el formulario, te encontrarás con un error familiar.

![Unknown action create for PostsController](http://edgeguides.rubyonrails.org/images/getting_started/unknown_action_create_for_posts.png)

Ahora necesitas crear la acción `create` en `PostsController` para que funcione.
