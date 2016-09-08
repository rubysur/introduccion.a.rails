Salvando datos en el controlador
================================

En `ArticlesController` necesitamos cambiar la acción `create` para usar el nuevo modelo `Article`
y guardar los datos en la base de datos. Abre `app/controllers/articles_controller.rb` y cambia la
acción `create` que debe verse de la siguiente manera:

```ruby
def create
  @article = Article.new(params[:article])

  @article.save
  redirect_to @article
end
```

Esto es lo que sucede: cada modelo Rails puede ser inicializado con sus respectivos
atributos, los cuales son automáticamente asignados a sus respectivas columnas de
base de datos. En la primera línea hacemos justamente eso (recuerda que
`params[:article]` contiene los atributos en los cuales estamos interesados). Luego,
`@article.save` es responsable de guardar el modelo en la base de datos. Finalmente,
direccionamos al usuario a la acción `show` que definiremos más tarde.

> **TIP:** Como veremos más tarde, `@article.save` devuelve un indicador que indica si el
modelo fue guardado o no.

Si recargas de nuevo la página http://localhost:3000/articles/new serás casi capaz de crear un nuevo artículo. Si lo pruebas, verás que se muestra este mensaje de error:

![ActiveModel::ForbiddenAttributesError](http://guides.rubyonrails.org/images/getting_started/forbidden_attributes_for_new_article.png)

Rails incluye varias opciones para ayudarte a desarrollar aplicaciones seguras y ahora mismo estás viendo
una de ellas. Esta opción se llama `strong_parameters` y obliga a decirle a Rails exactamente qué parametros estan disponibles en la accion de nuestros controladores.

Porque esto tiene que importarte? La capacidad de tomar y asignar todos los parámetros del controlador para su modelo automáticamente hace el trabajo del programador mas facil, pero por esta comodidad también permite un uso malintencionado. ¿Qué pasa si una solicitud al servidor fue diseñado para parecerse a un nuevo artículo, pero también incluyó campos adicionales con valores que violan la integridad de su aplicación? Serían "asignados en masa" en su modelo y luego en la base de datos junto con los buenos - esto puede potencialmente romper su aplicación, o peor.

Como en este caso sólo nos interesan los atributos `title` y `text`, debes añadir el siguiente método `article_params` y cambiar el código de la acción `create`:

```ruby
def create
  @article = Article.new(article_params)

  @article.save
  redirect_to @article
end

private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```
