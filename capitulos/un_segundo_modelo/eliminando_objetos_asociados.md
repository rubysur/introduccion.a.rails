Eliminando Objetos Asociados
============================

Si eliminas un artículo entonces sus comentarios asociados necesitas ser
eliminados también. Si no lo haces simplemente van a ocupar espacio en la base
de datos. Rails te permite usar la opción `dependent` en las asociaciones para
lograrlo. Modifica el modelo Post, en `app/models/post.rb`, de esta manera:

```ruby
class Post < ActiveRecord::Base
  validates :title, :presence => true,
                    :length => { :minimum => 5 }
  has_many :comments, :dependent => :destroy
end
```
