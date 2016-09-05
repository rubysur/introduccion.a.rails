Ejecutando una migración
========================

Como hemos visto, `rails generate model` crea un archivo _database
migration_ dentro del directorio `db/migrate`.
Las migraciones son clases de Ruby que están diseñadas para hacer simple la
creación y modificación de las tablas de la base de datos. Rails usa comandos rake
para ejecutar migraciones, y es posible deshacer una migración después de que ha sido aplicada
a la base de datos. Los archivos de migraciones incluyen una marca de la fecha y hora para
que sean procesadas en el orden que fueron creadas.

Si miras dentro del archivo `db/migrate/YYYYMMDDHHMMSS_create_articles.rb` (recuerda,
tu archivo puede tener un nombre ligeramente diferente), esto es lo que encontrarás:

```ruby
class CreateArticles < ActiveRecord::Migration[5.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :text

      t.timestamps
    end
  end
end
```

La migración de arriba crea un método llamado `change` el cual será llamado cuando ejecutes
la migración. La acción definida en este método es reversible, lo cual significa que Rails
conoce cómo deshacer los cambios realizados en esta migración en caso que necesites hacerlo
más tarde. Cuando ejecutas esta migración se creará una tabla `articles` con una columna tipo `string`
y otra columna tipo `text`. También crea dos campos de fecha-hora para permitir a Rails realizar
un seguimiento de las actualizaciones.

Mayor información acerca de las migraciones en Rails
puede ser encontrada en la guía [Rails Database Migrations](http://guides.rubyonrails.org/migrations.html).

En este punto, puedes usar el comando rake para ejecutar la migración:

```bash
$ rails db:migrate
```

Rails ejecutará este comando de migración y te responderá lo siguiente cuando haya
creado la tabla `articles`.

```bash
==  CreateArticles: migrating ==================================================
-- create_table(:articles)
   -> 0.0019s
==  CreateArticles: migrated (0.0020s) =========================================
```

> **Nota:** Debido a que estás trabajando en el ambiente de desarrollo por omisión,
este comando se aplicará a la base de datos definida en la sección `development`
de tu archivo `config/database.yml`. Si deseas ejecutar migraciones en otro
ambiente, por ejemplo en producción, debes indicarlo en forma explícita cuando
invoques el comando: `rails db:migrate RAILS_ENV=production`.
