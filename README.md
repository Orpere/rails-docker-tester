# git clone git@github.com:Orpere/rails-docker-tester.git  root of your project

## Update database.yaml on config as follow

```yaml
default: &default  
  adapter: postgresql  
  encoding: unicode  
  username: postgres  
  password:  
  pool: 5  
  host: db
production:  
  <<: *default  
  database: app_name_production
```

## Add this to your config/environments/production.rb

```ruby
add config.assets.compile = true
```

## If you are start the project from rails new just don't forget you don't have welcome in prod

```ruby
rails g controller welcome index

#add to routes.rb
Rails.application.routes.draw do
  get 'welcome/index'
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
  root 'welcome#index'
end
```

## Command line *

To build Containers =>  docker-compose build

To create a shema on Prod => docker-compose run app rake db:create RAILS_ENV=production

To popolate =>
docker-compose run app rake db:migrate db:seed RAILS_ENV=production

To Start => docker-compose up -d
