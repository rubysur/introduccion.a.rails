Agregando algunas validaciones
======================================

El archivo del modelo `app/models/article.rb` es tan simple como:

```ruby
class Article < ApplicationRecord
end
```

No hay mucho en ese archivo - pero nota que la clase `Article` hereda de
`ApplicationRecord`. `ApplicationRecord` hereda de `ActiveRecord::Base`
provee una gran cantidad de funcionalidad a los modelos de Rails de forma
sencilla, incluyendo las operaciones básicas CRUD (del inglés Create, Read,
Update, Destroy) de base de datos, validación de datos así como el soporte
a búsquedas sofisticadas y la habilidad de relacionar múltiples modelos
entre sí.

Rails incluye métodos que ayudaran a asegurar los campos de tu modelo.
Abre el archivo `app/models/article.rb` y complétalo de esta manera:

```ruby
class Article < ApplicationRecord
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```
Estos cambios asegurarán que todos los artículos tengan un título que sea al
menos de cinco caracteres de longitud. Rails puede validar una variedad de
condiciones en un modelo, incluyendo la presencia o la unicidad de columnas,
sus formatos y la existencia de objetos asociados. Las validaciones están cubiertas
en detalle en [Active Record Validations and Callbacks](http://guides.rubyonrails.org/active_record_validations.html).

Con las validaciones agregadas, cuando llames a `@article.save` en un artículo
inválido
retornará `false`. Si abres el archivo `app/controllers/articles_controller.rb`
otra vez, notarás que no verificamos el resultado de la llamada `@article.save`
dentro de la acción `create`. Si `@article.save` falla en esta situación, necesitamos mostrar
el formulario de regreso al usuario. Para hacer esto, cambiar las acciones `new` y `create`
dentro de `app/controllers/articles_controller.rb` a esto:

```ruby
def new
  @article = Article.new
end

def create
  @article = Article.new(article_params)

  if @article.save
    redirect_to @article
  else
    render 'new'
  end
end

private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

La acción `new` está ahora creando una nueva instancia llamada `@article`,
y verás el motivo de ello en un momento.

Notas que dentro de la acción `create` usamos `render` en lugar de `redirect_to` cuando acción `save`
retorna `false`. El método `render`es usado de manera que el objeto `@article`es regresado a la plantilla
`new` cuando es interpretado. Esta interpretación se hace dentro de la misma solicitud que hace el envío
del formulario, mientras que `redirect_to`le dirá al navegador para emitir una nueva solicitud.

Si recargas [http://localhost:3000/articles/new](http://localhost:3000/articles/new) y
tratas de guardar un artículo sin título, Rails enviará de regreso un formulario
pero que no es muy útil. Necesitas decirle al usuario que algo está mal.
Para hacer esto hay que modificar el archivo `app/views/articles/new.html.erb`
para verificar los mensajes de error:

```html+erb
<%= form_for :article, url: articles_path do |f| %>

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

Veamos qué está pasando. Verificamos si hay errores con
`@article.errors.any?` y en caso que los haya mostramos una lista de todos
los errores con `@article.errors.full_messages`.

`pluralize` es un asistente de Rails que toma un número, un texto y sus argumentos.
Si el número es mayor de 1, el texto será automáticamente pluralizado

La razón de por qué agregamos `@article = Article.new` en `ArticlesController`
es que de otra manera `@article` será `nil` en tu vista y llamar a
`@article.errors.any?` mostrará un error.

CONSEJO: Rails automaticamente ajustará los campos que contienen error en un `div`
dentro de la clase `field_with_errors`. Puedes definir una regla `css` para destacarlos.

Ahora verás un bonito mensaje de error cuando intentes guardar un artículo sin título
en [new post form (http://localhost:3000/articles/new)](http://localhost:3000/articles/new).

![Form With Errors](http://guides.rubyonrails.org/images/getting_started/form_with_errors.png)
