Profundizando en REST
=====================

Ya hemos cubierto todas las acciones CRUD de una aplicación REST.
Lo hicimos declarando rutas separadas con los verbos adecuados en
`config/routes.rb`. Así es como se ve el archivo hasta ahora:

```ruby
get "posts" => "posts#index"
get "posts/new"
post "posts" => "posts#create"
get "posts/:id" => "posts#show", :as => :post
get "posts/:id/edit" => "posts#edit"
put "posts/:id" => "posts#update"
delete "posts/:id" => "posts#destroy"
```

Eso es un montón de código para cubrir un único **recurso**. Afortunadamente,
Rails proporciona un método llamado `resources` el cual puede ser usado para
declarar un recurso REST estándar. Así es como el archivo `config/routes.rb`
se ve luego de utilizar `resources`:

```ruby
Blog::Application.routes.draw do

  resources :posts

  root :to => "welcome#index"
end
```

Si ejecutas `rake routes`, podrás ver que todas las rutas que
declaramos anteriormente aún están disponibles:

```bash
# rake routes
    posts GET    /posts(.:format)          posts#index
          POST   /posts(.:format)          posts#create
 new_post GET    /posts/new(.:format)      posts#new
edit_post GET    /posts/:id/edit(.:format) posts#edit
     post GET    /posts/:id(.:format)      posts#show
          PUT    /posts/:id(.:format)      posts#update
          DELETE /posts/:id(.:format)      posts#destroy
     root        /                         welcome#index
```

Además, si vas a través de las acciones de creación, actualización
y eliminación de posts, la aplicación sigue funcionando como antes.

TIP: En general, Rails fomenta el uso de recursos (`resources`) en lugar
de declarar las rutas manualmente. Se hizo solamente en esta guía como
un ejercicio de aprendizaje. Para más información acerca de _routing_,
mira [Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html).
