---
layout: post
category : Ruby on Rails
tagline: "Supporting tagline"
tags : [Ruby on Rails]
---
{% include JB/setup %}

Devise is a very useful and common gem for User Authentication and Authorization in Ruby on Rails.

### Installation

Search 'devise' in Ruby gem library, copy the latest virsion for gemfile.

Add `gem 'devise', '~> 4.2'` to `Gemfile` in Project.

Then run `bundle install` to install the gem.

### Getting started

Next, run generator: `rails generate devise:install`. A couple of instructions will show in the console, simply follow the instructions.

After configuration, run `rails generate devise MODEL`, where `MODEL` is your model name for users (usually begin called 'User' or 'Admin').

Run `rake db:migrate` to migrate the new user table.

### How to use for authorization?

Devise gem will generate a couple of views for user to `sign up `, `sign in`, `sign out` etc. Which are in `host:3000/User/Sign_up` etc. For details, run `rails routes` to check the path.

#### Authorization

Add `before_action :authenticate_user!` in the top of controller page, after 
`before_action :set_post, only: [:show, :edit, :update, :destroy]`. This will tell Rails this controller can only be visited if a user being authorized. 

If some of the methods do not need to be authorized, simply add `except: [:methodName]` after the code.

#### Heplers

To verify if a user is signed in:
`user_signed_in?`
Get the current signed_in user:
`current_user`
Access session for this scope:
`user_session`

Those will help you get user information no matter in controller or in views.

### Customerization

#### Views

`rails generate devise:views`
Run this and Devise gem will generate the views for user to let you customize the views.

For more details: [https://github.com/plataformatec/devise](https://github.com/plataformatec/devise)
