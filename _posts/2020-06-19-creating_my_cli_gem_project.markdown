---
layout: post
title:      "Creating my CLI Gem project  "
date:       2020-06-19 17:01:27 +0000
permalink:  creating_my_cli_gem_project
---


My first step is to look for an api (Application Programming Interface)   
 using HTTparty gem to get my data. and install  Type gem install httparty on your terminal to install and gem install  pry.(binding.pry) after istalling you need to require both gem.

```
 require “httparty” 
 require “pry"


 url = "https://www.themealdb.com/api/json/v1/1/search.php?s”
  response = HTTParty.get(url)
   meals_array = response["meals"] 
 
 ```


 This line of code is where I set the response to a variable = meals_array and grabing the “meals” string
  and iterate with #each. setting a binding.pry to get the data in the terminal.
		
 ```
 meals_array.each do |meal_hash| 
      #binding.pry 
    end 
		
```
		
		
Now its time to install Bundle gem, 
in my terminal I type bundle gem meals, meals is the name of my model class. 
This command creates a scaffold directory for my new gems.  

in my ‘Bin' directory I  created run/executable  file

Bin 
  > run file where I require my environment file
  
```

#!/usr/bin/env ruby  => this line of code is called shebang!(explicitly telling to execute Ruby)

require_relative "../lib/environment” 


```

My Environment file. Where I require all my dependencies and classes. 

```
require_relative "./meals/version" 

require "pry" 
require "httparty"

require_relative "./api.rb" 
require_relative "./the_meals.rb"
require_relative "./cli.rb"


```

and my Lib directory I created 3 files Cli.rb, Api.rb, Meals.rb

Lib 
 > cli.rb => My Cli class were I cummunicate with my user. all my input and output command should be in this class
 
```
class Meals::Cli  
   
    def menu 
        puts "----------------- Menu -----------------------"     
        puts "Type: '1' to see the menu of International meals"  
        puts "Type: '2' to exit the menu" 
        puts "" 
        puts "———————————————————————“
    end
ennd
```


 > Api.rb =>
 >  My Api class
 >  where I consume the api or get my data( url="https://www.themealdb.com/api/json/v1/1/search.php?s”)

```
Class Meal::Api

 url = "https://www.themealdb.com/api/json/v1/1/search.php?s"
 response = HTTParty.get(url)
 meals_array = response["meals”]
  
end
```


> Meals.rb => is my  model class 

```
class Meals::TheMeals
   
     @@all = []
		 
     attr_accessor :name

     def initialize(name)
         @name = name
         @@all << self
     end 
     
     def self.all
         @@all
     end
 end 

```

Files below are automaticlly created by bundle gem 

License
Read me  
Gem file
Rakefile 
Gemspec 
Code of conduct 


