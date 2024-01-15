```
gem "devise"
gem "omniauth"
gem "omniauth-google-oauth2"
gem "omniauth-rails_csrf_protection"
```

```
rails g devise:install
```

## add this file to config/initializers/devise.rb
```
  config.mailer_sender = 'please-change-me-at-config-initializers-devise@example.com'
  config.omniauth :google_oauth2, ENV['GOOGLE_OAUTH_CLIENT_ID'], ENV['GOOGLE_OAUTH_CLIENT_SECRET']
  
```
## create model
```
rails g devise User
```

```


## add this to app/models/user.rb
```
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  <!-- devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable -->
         :omniauthable, omniauth_providers: [:google_oauth2]
end


## add this to the migration devise file 

```
class DeviseCreateUsers < ActiveRecord::Migration[7.1]
  def change
    create_table :users do |t|
      ## Database authenticatable
      <!-- t.string :email,              null: false, default: ""
      t.string :encrypted_password, null: false, default: "" -->
      t.string :full_name
      t.string :uid 
      t.string :avatar_url
      t.string :provider```


```
rails db:migrate
```


## add this to the route file

```
Rails.application.routes.draw do
  <!-- resources :posts -->
  devise_for :users, controllers: {
    registrations: "users/registrations",
    sessions: "users/sessions",
    omniauth_callbacks: "users/omniauth_callbacks"
  }```


  ```
  rails g devise:controllers users
  ```

  ## addi this to controllers.users/sessions_controller.rb
  ```
   def after_sign_out_path_for(resource_or_scope)
    new_user_session_path
  end
   def after_sign_in_path_for(resource_or_scope)
    stored_location_for(resource_or_scope) || root_path 
  end
  ```

  ## add this to models/user.rb
  ```

class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable,
         :omniauthable, omniauth_providers: [:google_oauth2]
def self.from_omniauth(auth)
  where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
    user.email = auth.info.email
    user.password = Devise.friendly_token[0,20]
    user.full_name = auth.info.name  # assuming the user model has a name
    user.avatar_url = auth.info.image # assuming the user model has an image
    # if you are using confirmable and the provider(s) you use validate emails, 
    # uncomment the line below to skip the confirmation emails.
    # user.skip_confirmation!
  end
end
end 
```
## add this to controllers/users/omniauth_callbacks_controller.rb
```
# frozen_string_literal: true

class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController

  def google_oauth2
    user = User.from_omniauth(auth)
  end 


  def auth
    @auth || request.env['omniauth.auth']
  end
end
```













# add credentials to config/credentials.yml.enc
```
EDITOR="code --wait" rails credentials:edit
```




# This one is working
```
m@m-HP-EliteBook-840-G4:~/pro/ethio-computer-skill$ EDITOR=nano rails credentials:edit
Editing config/credentials.yml.enc...
File encrypted and saved.
m@m-HP-EliteBook-840-G4:~/pro/ethio-computer-skill$ 

```

rails g devise:views

