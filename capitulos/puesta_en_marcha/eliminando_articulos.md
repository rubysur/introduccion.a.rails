Eliminando artículos
====================

Ahora estamos listos para cubrir la parte "D" del acrónimo CRUD: eliminar artículos
de la base de datos. Siguiendo la convención REST, vamos a agregar una ruta para la
eliminación de artículos a `config/routes.rb`:

```ruby
delete "posts/:id" => "posts#destroy"
```
El método de enrutamiento `delete` debe ser usado para métodos que destruyen recursos.
Si se deja como un típico comando de ruteo `get`, es posible que se puedan enviar
URLs malintencionadas como estas:

```html
<a href='http://yoursite.com/posts/1/destroy'>look at this cat!</a>
```

Nosotros usamos el método `delete` para destruir recursos y este ruteo está enlazado
con la acción `destroy` dentro de `app/controllers/posts_controller.rb`, la cual no existe
aún pero que se muestra a continuación:

```ruby
def destroy
  @post = Post.find(params[:id])
  @post.destroy

  redirect_to :action => :index
end
```

Puedes llamar a `destroy` en objetos Active Record cuando desees eliminarlos de la
base de datos. Hay que tener en cuenta que no necesitas agregar una vista para esta acción ya que
estamos siendo redireccionados a la acción `index`.

Finalmente, agregamos un enlace a la plantilla de la acción `index`
(`app/views/posts/index.html.erb`) para completar todo.

```html+erb
<h1>Listing Posts</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
    <th></th>
    <th></th>
  </tr>

<% @posts.each do |post| %>
  <tr>
    <td><%= post.title %></td>
    <td><%= post.text %></td>
    <td><%= link_to 'Show', :action => :show, :id => post.id %></td>
    <td><%= link_to 'Edit', :action => :edit, :id => post.id %></td>
    <td><%= link_to 'Destroy', { :action => :destroy, :id => post.id }, :method => :delete, :data => { :confirm => 'Are you sure?' } %></td>
  </tr>
<% end %>
</table>
```
Usaremos aquí `link_to` de diferente manera. Empaquetaremos los atributos
`:action` y `:id` en un hash de manera que podamos pasar las dos claves como uno
en un solo argumento y finalmente las otras dos claves como otro argumento.
Las opciones `:method` `:data` y `:confirm` son usadas como atributos HTML de manera de que cuando
se hace clic en el enlace Rails mostrará un diálogo de confirmación al usuario
y luego direccionará al enlace con el método `delete`.
Esto es realizado a través de un archivo JavaScript `jquery_ujs` el cual fue automáticamente
incluido dentro del diseño de tu aplicación (`app/views/layouts/application.html.erb`) cuando
la aplicación fue generada. Sin este archivo, el diálogo de confirmación no aparecerá.

![Confirm Dialog](http://edgeguides.rubyonrails.org/images/getting_started/confirm_dialog.png)

Felicitaciones, ahora puedes crear, mostrar, enumerar, actualizar y eliminar
artículos. En la siguiente sección veremos cómo Rails puede ayudarnos en la creación de
aplicaciones REST, y cómo podemos refactorizar nuestro Blog  para tomar
ventaja de ello.
