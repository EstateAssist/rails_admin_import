Gem Reboot
========

I took over development on this gem. Please report new issues and I'll address them. Julien Vanier


Rails Admin Import functionality
========

Plugin functionality to add generic import to Rails Admin interface

Installation
========

* First, add to Gemfile:
    
        gem "rails_admin_import"

* Next, mount in your application by adding following line to your config/routes.rb:

        mount RailsAdminImport::Engine => '/rails_admin_import', :as => 'rails_admin_import'

* If you are using cancan, add to ability.rb to specify which models can be imported:

        can :import, [User, Model1, Model2]

* Define configuration in config/initializers/rails_admin_import.rb:

        RailsAdminImport.config do |config| 
          config.model User do
            excluded_fields do
              [:field1, :field2, :field3]
            end
            label :name
            extra_fields do
              [:field3, :field4, :field5]
            end
          end
        end

* (Optional) Define instance methods to be hooked into the import process, if special/additional processing is required on the data:

        # some model
        def before_import_save(row, map)
          # Your custom special sauce          
        end

        def after_import_save(row, map)
          # Your custom special sauce          
        end

You could for example set an attribute on a Devise User model to skip checking for a password when importing a new model.

You could also download a file based on a URL from the import file and set a Paperclip file attribute on the model.

* "import" action must be added inside config.actions block in main application RailsAdmin configuration: config/initializers/rails_admin.rb.

        config.actions do
          ...
          import
          ...
        end

  Refer to [RailAdmin documentation on custom actions](https://github.com/sferik/rails_admin/wiki/Actions) that must be present in this block.


* TODO: Right now, import doesn't work for fields ending in s, because inflector fails in models ending in s singularly. Belongs_to and many
  mapping needs to be updated to use klasses instead of symbols

TODO
========

* Testing

Copyright
========

Copyright (c) 2014 End Point & Steph Skardal. See LICENSE.txt for further details.
