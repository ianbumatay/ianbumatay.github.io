---
layout: post
title:      "Quick guide in creating sinatra application "
date:       2020-08-18 13:46:16 -0400
permalink:  quick_guide_in_creating_sinatra_application
---

this is a quick guid in building  directory and files in my sinatra portfolio project.

 **what is sinatra **

Sinatra is a free and open source software web application library and domain-specific language written in Ruby. It is an alternative to other Ruby web application frameworks such as Ruby on Rails, Merb, Nitro, and Camping. It is dependent on the Rack web server interface. It is named after musician Frank Sinatra.

what is  (DSL) 

A domain-specific language (DSL) is a computer language specialized to a particular application domain.  

First, make sure Sinatra is installed by running `gem install sinatra`  in your terminal. 


### File and Directories

**Using Corneal gem to generate my application**

Corneal is gem created by a former Flatiron student named Brian Emory.  that build a Sinatra skeleton similar to running 
`rails new APP-NAME` in rails. 

**To generate your app:** 

 Install the gem

`corneal new APP-NAME`

 After Corneal is done generating your app, run bundle install from your app's directory:

 `$ cd APP-NAME`
			 

 `$ bundle install`

You can then start your server with shotgun: after running check localhost 9393 in your browser.

   `$ shotgun` 

[corneal](https://github.com/thebrianemory/corneal) click to learn more about corneal gem.


### Database

 run `$  rake db:create_migration NAME=create_bullitins ` to create table 

 after creating the table I run `rake db:migrate` this will create .schema the in db: directory(database) 
 
**using corneal to generate migration.**
 
  You can generate a model and migration file:

  corneal model NAME

  You can also generate an entire MVC structure complete with a migration file:

	corneal scaffold NAME
	
 
 ### Controllers < Sinatra: :Base

 application_controller < Sinatra: :Base 

 models_controller < application_controller 


 ### Models < ActiveRecord: :Base
  
 `class Bullitin belongs_to :user`  (association)
					
 `class User has_many: bullitins` (association)
          
  `validates :title, :content,  presence: true  (validation) 
	
	### config.run    
	
	this is important to remember 
	
 use Rack::MethodOverride
 
 use BullitinsController
 use UsersController
 run ApplicationController


 ### Views 
 
  containes .erb files:  
	
### password security 
	
install gem 'bcrypt' 
	
set table attribute as password_digest:

t.string :password_digest 

in User_model  set macro: has_secure_password 

$ rake console to test


### sessions

enable session in app/application_controller 

```ruby
configure do 

enable :sessions 

end 
```
				
### validation  
for more understanding on validation [guides](https://guides.rubyonrails.org/active_record_validations.html)

			
  
	
	 

				   
			 
			 
                         				                
         
          
							 
 





The content of your blog post goes here.
