Creando un nuevo post
=====================

Ahora que has visto cómo crear un controlador, una acción y una vista, vamos a crear
algo con un poco más de sentido.

En la aplicación de Blog, tú vas a crear un nuevo recurso (_resource_). Un recurso
es el término usado para una colección de objetos similares, como posts, personas o
animales. Tú puedes crear, leer, actualizar y eliminar objetos para un recurso
y estas operaciones son referidas como operaciones _CRUD_.

Rails proporciona un método (_resource_) que se puede utilizar para declarar un recurso REST estándar.
Es necesario agregar el recurso (_article_) en `config/routes.rb` el archivo se verá de la siguiente manera:

```ruby
Blog.application.routes.draw do
  resources :articles

  root 'welcome#index'
end
```
Si ejecutas `rails routes` veras que se han definido rutas para todas las acciones estandar de RESTful.
El significado de la columna _prefix_ (y otras columnas) los veremos mas adelante, lo importante es notar
que Rails ha inferido la palabra en singular del recurso articles es article, con lo que el resultado es el siguiente:

```bash
$ bin/rails routes
      Prefix Verb   URI Pattern                  Controller#Action
    articles GET    /articles(.:format)          articles#index
             POST   /articles(.:format)          articles#create
 new_article GET    /articles/new(.:format)      articles#new
edit_article GET    /articles/:id/edit(.:format) articles#edit
     article GET    /articles/:id(.:format)      articles#show
             PATCH  /articles/:id(.:format)      articles#update
             PUT    /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy
        root GET    /                            welcome#index
```

En la siguiente sección, tú añadirás la habilidad de crear nuevos posts en tu aplicación
y poder verlos también. Ésto es la "C" y la "R" de _CRUD_: creación y lectura. La manera
de hacer esto se vería de la siguiente manera:

![The new post form](http://guides.rubyonrails.org/images/getting_started/new_article.png)

Se ve un poco básico por ahora, pero está bien. Ya veremos cómo mejorar el estilo.
