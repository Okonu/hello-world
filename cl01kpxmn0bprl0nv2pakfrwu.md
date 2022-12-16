# Deploying Ruby on Rails 7 to Heroku

## Introduction

Ruby on Rails just updated its version from rails 6 to 7.0.1, which is slightly different from the previous version. We won't require webpacker anymore, and there are a number of other improvements that make rails more efficient. To run Rails 7 alpha, you should have Ruby 3.0.1 installed. When working on rails projects, it's best to utilize Linux or Mac environments; but, if you're using Windows, you can install [WSL](https://docs.microsoft.com/en-us/windows/wsl/install). This tutorial will primarily cover Ubuntu 20.04.


##Prerequisities
* [Ubuntu 20.04 installed on your cloud server at](https://my.vultr.com/deploy/) with at least 4 GB RAM
* Basic HTML, Postgresql, Ruby and Rails Skills
* Basic Ubuntu Terminal use knolwedge
* Ruby and Ruby on Rails installed.
>Run the following command to check:

    $ rbenv -v 
    rbenv 1.1.2-61-g585ed84
    $ ruby -v 
     ruby 2.7.1p83 (2020-03-31 revision a0c7c23c9c)  x86_64-linux] 
    $ rails -v
    Rails 6.1.4.1
>[How to install Ruby and Ruby on  Rails in Ubuntu](https://www.vultr.com/docs/install-ruby-with-rvm-on-ubuntu-18-04-and-19-10)

## 1. Getting Started
* Modify  `gem 'rails'` to  `gem 'rails' , github: 'rails/rails'` to upgrade to Rails 7 alpha from Rails 6.1.4.1 then run:
    
		$bundle	
		#then check the version of rails
		$ rails -7
		Rails 7.1.0.alpha

## 2. Webpacker Project Initializing: Blog project.

>In this article we will create a blog project to deploy on Heroku using Ruby. You can skip the Blog project part and >use your own project. 

Run the following instructions and go to ruby to install the ruby gems that will be required to get started with the project:

    $ rails new my-rails7-blogapp --main --css=bulma --database=postgresql
		$ gem install cssbundling-rails
    $ gem install importmap-rails
    $ gem install stimulus-rails
    $ gem install turbo-rails

## 3. Building the Blog Project
### 3.1 Setting up Postgresql database
    
		$ sudo -u postgres psql
    postgress=# CREATE USER rails7 WITH PASSWORD 'rails7';
    CREATE ROLE
    postgress=# CREATE DATABASE railsdb;
    CREATE DATABASE
		posgres=# GRANT ALL PRIVILEGES ON DATABASE "railsdb";
		GRANT

make modifications to the database, username, and password in your database.yml file;
    
		#open config/database.yml
		#PostgreSQL. Versions 9.3 and up are supported.
		#
		#Install the pg driver:
		#gem install pg
		#
		development:
		  adapter: postgresql
      encoding: unicode
      host: localhost
      database: railsdb
		#For details on connection pooling, see Rails configuration guide
		#  <https://guides.rubyonrails.org/configuring.html#database-pooling>
		  pool: 5
      timeout: 5000
      username: rails7
      password: rails7
		
		#The specified database role being used to connect to postgres.
    #To create additional roles in postgres see `$ createuser --help`.
    #When left blank, postgres will use the default role. This is
    #the same name as the operating system user running Rails.
    #username: twitter_redesign

    #The password associated with the postgres role (username).
    #password:

    #Connect on a TCP socket. Omitted by default since the client uses a
    #domain socket that doesn't need configuration. Windows does not have
    #domain sockets, so uncomment these lines.
    #host: localhost

    #The TCP port the server listens on. Defaults to 5432.
    #If your server runs on a different port number, change accordingly.
    #port: 5432

    #Schema search path. The server defaults to $user,public
    #schema_search_path: myapp,sharedapp,public

    #Minimum log levels, in increasing order:
    #debug5, debug4, debug3, debug2, debug1,
    #log, notice, warning, error, fatal, and panic
    #Defaults to warning.
    #min_messages: notice

    #Warning: The database defined as "test" will be erased and
    #re-generated from your development database when you run "rake".
    #Do not set this db to the same as development or production.
    test:
      adapter: postgresql
      encoding: unicode
      host: localhost
      database: railsdb
      pool: 5
      timeout: 5000
      username: rails7
      password: rails7
    #As with config/credentials.yml, you never want to store sensitive information,
    #like your database password, in your source code. If your source code is
    #ever seen by anyone, they now have access to your database.
		#
		# Instead, provide the password or a full connection URL as an environment
    #variable when you boot the app. For example:
		#
		#  DATABASE_URL="postgres://myuser:mypass@localhost/somedatabase"
		#
		#If the connection URL is provided in the special DATABASE_URL environment
    #variable, Rails will automatically merge its configuration values on top of
    #the values provided in this file. Alternatively, you can specify a connection
    #URL environment variable explicitly:
		#
		production:
      url: <%= ENV['MY_APP_DATABASE_URL'] %>
		#
		# Read https://guides.rubyonrails.org/configuring.html#configuring-a-database
    # for a full overview on how database connection configuration can be specified.
		#
		# production:
    #  <<: *default
    #  database: twitter_redesign_production
    #  username: twitter_redesign
    #  password: <%= ENV['TWITTER_REDESIGN_DATABASE_PASSWORD'] %>

Run this command to start the Rails Server:
    
    $rails server

Continuing to build the blog:
    bin/rails generate controller Articles index --skip-routes

### 3.2. Running Migrations
    $ bin/rails generate model Article title:string body:text
    $ bin/rails db:migrate
    # run migration to come up with this
    # == 20211216113128 CreateArticles: migrating #===============================
    # -- create_table(:articles)
     #  -> 0.3481s
    #== 20211216113128 CreateArticles: migrated 
     # (0.3492s) ======================
this will generate new migrations on db/migrate/folder

### 3.3. Generating Routes
 
config/routes.rb

    Rails.application.routes.draw do
      root "articles#index"

      resources :articles
    end

    $ bin/rails routes


### 3.4 Views

 app/views/articles/index.html

    <h1>Articles</h1>
    <ul>
        <% @articles.each do |article| %>
            <li>
                <%= link_to article.title, article %>
            </li>
        <% end %>
    </ul>

    <%= link_to "New Article", new_article_path %>

app/views/articles/show.html

    <h1><%= @article.title %></h1>

    <p><%= @article.body %></p>


    <ul>
      <li><%= link_to "Edit", edit_article_path(@article) %></li>
      <li><%= link_to "Destroy", article_path(@article),
                      method: :delete,
                      data: { confirm: "Are you sure?" } %></li>
    </ul>

app/views/articles/_form.html.erb

    <%= form_with model: article do |form| %>
        <div>
          <%= form.label :title %><br>
          <%= form.text_field :title %>
          <% article.errors.full_messages_for(:title).each do |message| %>
            <div><%= message %></div>
          <% end %>
            </div>

        <div>
          <%= form.label :body %><br>
          <%= form.text_area :body %><br>
          <% article.errors.full_messages_for(:body).each do |message| %>
            <div><%= message %></div>
          <% end %>
        </div>

        <div>
          <%= form.submit %>
        </div>
      <% end %>

app/views/articles/new.html

    <h1>New Article</h1>

    <%= render "form", article: @article %>

app/views/articles/edit.html
    
    <h1>Edit Article</h1>

    <%= render "form", article: @article %>

### 3.5. Models

app/models/article.rb

    class Article < ApplicationRecord
        validates :title, presence: true
      validates :body, presence: true, length: { minimum: 10 }
    end

### 3.6. Controllers

app/controllers/articles_controlle.rb

    class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
    @article = Article.find(params[:id])
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit, status: :unprocessable_entity
    end
  end

  def destroy
    @article = Article.find(params[:id])
    @article.destroy

        redirect_to root_path
      end

      private
        def article_params
          params.require(:article).permit(:title, :body)
        end
    end

To see a live version of the article in the browser, type '$ rails s'.


## 4. Set up a Github Repository
It's a good idea to set up your GitHub repository and commit your code as we'll be deploying our project to Heroku.
* Create a new repository on your Github account. 
* Open the project in your code editor, 
* Run the commands for creating a new repository in the terminal  (follow the commands in your GitHub repository);
    
		$git init 
		$ git add . 
		$ git commit -m "Add Initial Files" 
		$ git branch -M main
		$ git remote add origin https://github.com/username/repository_name.git  
		$ git push -u origin main

## 5. Using Heroku

* You'll need to [sign up for a Heroku account or login in](https://www.heroku.com) to an existing account on the Heroku Website with the same email address you used on git/Github.
* Set up Heroku CLI by using the instructions below to configure the Heroku command line:

    curl https://cli-assets.heroku.com/install.sh | sh

checking the Heroku Version
*  Heroku will ask for your SSH key. This establishes a connection between your system and your Heroku account.

    heroku keys:add 
    ## For Heroku to upload your public SSH key, press y and Enter. 

### 5.1 Heroku Deployment

    $ heroku login
    ## browser opened up
    $ heroku create
    $ git config --list --local | grep heroku
    $ git push heroku main



  