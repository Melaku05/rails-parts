Deploying a Ruby on Rails application on DigitalOcean involves several steps. Here's a general guide:

1. **Create a Droplet on DigitalOcean**: Choose an image that includes Ruby, Rails, and PostgreSQL. You can also choose a plain Ubuntu image and install these yourself.

2. **Set up your environment**: If you chose a plain Ubuntu image, you'll need to install Ruby, Rails, and PostgreSQL. You can use RVM or rbenv to manage Ruby versions.

3. **Clone your application**: Clone your application from your version control system to your droplet.

4. **Install dependencies**: Run `bundle install` to install your Ruby dependencies, and `yarn install` to install your JavaScript dependencies.

5. **Set up the database**: Run `rails db:create db:migrate` to create and migrate your database.

6. **Precompile assets**: Run `rails assets:precompile` to precompile your assets.

7. **Set up environment variables**: If your application uses environment variables, set these up on your droplet.

8. **Set up a web server**: Install a web server like Nginx or Apache, and configure it to serve your Rails application.

9. **Set up a process manager**: Install a process manager like Phusion Passenger or Puma to manage your Rails processes.

10. **Start your application**: Start your Rails application using your process manager.

11. **Set up a reverse proxy**: Configure your web server to act as a reverse proxy for your Rails application.

12. **Set up SSL**: If you want to use HTTPS, set up SSL using Let's Encrypt.

13. **Set up a firewall**: Set up a firewall using ufw or iptables to secure your droplet.

14. **Set up regular backups**: Set up regular backups to ensure that you don't lose any data.

Remember, this is a general guide and the exact steps may vary depending on your application and your specific requirements. It's also a good idea to automate these steps using a provisioning tool like Ansible, Chef, or Puppet.




```
sudo apt-get update
```


```
sudo apt-get install postgresql postgresql-contrib
```


```
sudo -u postgres psql

```


```
CREATE ROLE your_username WITH LOGIN PASSWORD 'your_password';
```


```
GRANT ALL PRIVILEGES ON DATABASE your_database TO your_username;
```


```
config/database.yml
```

#
default: &default
  adapter: postgresql
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  timeout: 5000

development:
  <<: *default
  database: storage_development_postgres
  username: postgres
  password: Melaku11@#
# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: storage/test_postgres
  username: postgres
  password: Melaku11@#

production:
  <<: *default
  database: storage_production.postgres
  username: <%= ENV['DATABASE_USERNAME'] %>
  password: <%= ENV['DATABASE_PASSWORD'] %>
  host: localhost
  port: 5432


``` 

bundle install
```

```
rails db:migrate
```

```
sudo -u postgres psql
CREATE DATABASE storage_production_postgres;
GRANT ALL PRIVILEGES ON DATABASE storage_production_postgres TO your_username;
ALTER USER postgres PASSWORD 'new_password';
```

```
sudo apt-get install git curl libssl-dev libreadline-dev zlib1g-dev  autoconf bison build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev libgdbm-dev

```


```
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```

```
rbenv install 3.2.2
rbenv global 3.2.2

```


```
gem install rails
```

```
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```


```
git clone git@github.com:msiganasoftwaredesigners/Etl_landing_page.git
```

``` 

bundle install
```

``` 
EDITOR="nano" rails credentials:edit
```

``` 
rm config/credentials.yml.enc
``` 

```
production:
  database:
    username: your_username
    password: your_password
    ```


    ```
sudo -u postgres psql -c "SHOW hba_file;"
```

```
sudo nano /etc/postgresql/versionofpostgres/main/pg_hba.conf
```

```
# TYPE  DATABASE        USER            ADDRESS                 METHOD
local   all             postgres                                peer to md5




```
sudo service postgresql restart
```

```
psql -U postgres -h localhost -d storage/development_postgres
````

```

GRANT ALL PRIVILEGES ON DATABASE storage_development_postgres TO postgres;
```


```
sudo apt-get install nginx

```

``` 
sudo nano /etc/nginx/sites-available/your_app
```


```
server {
  listen 80;
  server_name your_domain.com;
  root /path/to/your/app/public;

  location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}
```

```
p
```
    
```
sudo ln -s /etc/nginx/sites-available/your_app /etc/nginx/sites-enabled/your_app
```

```
sudo nginx -t
```

```
sudo systemctl restart nginx
```

```
config/puma.rb
```

```
workers Integer(ENV['WEB_CONCURRENCY'] || 2)
threads_count = Integer(ENV['RAILS_MAX_THREADS'] || 5)
threads threads_count, threads_count

preload_app!

rackup      DefaultRackup
port        ENV['PORT']     || 3000
environment ENV['RACK_ENV'] || 'development'

on_worker_boot do
  ActiveRecord::Base.establish_connection
end
```

```
bundle exec puma -C config/puma.rb
```


```
var/www/Etl_landing_page/public
```

```
server {
  listen 80;
  server_name 144.126.220.97;
  root /var/www/Etl_landing_page/public;

  location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}
    
    ```
    
    ```screen -S rails
    ```
    
    
    ```
    bundle exec puma -C config/puma.rb
    ```
    
    ``` 
    ctrl + a  then d
    ```
    
    ## To stop the appliation

    ```
    screen -rails
    ```
    
    ```
    ctrl + c
    ```
    
    ```

   ## change for the IP address to the domain name (ethiolanguages.com)
    ```
    ```
    ```

    ```
    root@etl-page:/var/www/Etl_landing_page/config/environments# nano production.rb
    ```
    
    ```
    # Enable DNS rebinding protection and other `Host` header attacks.
  config.hosts = [
    "ethiolanguages.com",     # Allow requests from example.com
    "www.ethiolanguages.com"  # Allow requests from subdomains like `www.example.com`
  ]
  # Skip DNS rebinding protection for the default health check endpoint.
    ```

    ```
    require_relative "boot"

require "rails/all"

Bundler.require(*Rails.groups)

module EtlPage
  class Application < Rails::Application
  
    config.load_defaults 7.1

   
    config.autoload_lib(ignore: %w(assets tasks))

   
    config.hosts << "ethiolanguages.com"
    config.hosts << "www.ethiolanguages.com"
  end
end```

```
ls /etc/nginx/sites-available/
```

```server {
    listen 80;
    server_name ethiolanguages.com www.ethiolanguages.com;

    location / {
        proxy_pass http://localhost:3000; # assuming your Rails app is running on port 3000
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
```
sudo nginx -t
sudo service nginx restart
``````