Salvando datos en el controlador
================================

En `posts_controller` necesitamos cambiar la acción `create` para usar el nuevo modelo `Post`
y guardar los datos en la base de datos. Abra el archivo y cambie la acción `create`
que debe verse de la siguiente manera:

```ruby
def create
  @post = Post.new(params[:post])

  @post.save
  redirect_to :action => :show, :id => @post.id
end
```

Esto es lo que sucede: cada modelo Rails puede ser inicializado con sus respectivos
atributos, los cuales son automáticamente asignados a sus respectivas columnas de
base de datos. En la primera línea hacemos justamente eso (recuerda que
`params[:post]` contiene los atributos en los cuales estamos interesados). Luego,
`@post.save` es responsable de guardar el modelo en la base de datos. Finalmente,
direccionamos al usuario a la acción `show` que definiremos más tarde.

> **TIP:** Como veremos más tarde, `@post.save` devuelve un indicador que indica si el
modelo fue guardado o no.
