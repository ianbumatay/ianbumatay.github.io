---
layout: post
title:      "Creating my CLI Data Gem project  "
date:       2020-06-19 13:01:28 -0400
permalink:  creating_my_cli_gem_project
---


My first step is to look for an API (Application Programming Interface) installed  HTTparty gem to get my data. 
 
*   install httparty on your terminal . 
*   install  pry.(binding.pry)
*    after istalling you need to require both gem.
*    assign url = your API 

```
     require “httparty” 
     require “pry"


     url = "https://www.themealdb.com/api/json/v1/1/search.php?s”
     response = HTTParty.get(url)
     meals_array = response["meals"] 
 
 ```

*  This line of code is where I set the response to a variable = meals_array 
*   iterate with #each.
*    setting a binding.pry to get the data in the terminal.
		
 ```
 meals_array.each do |meal_hash| 
      #binding.pry 
    end 
		
```
		
		
Now its time to install a gem bundler.

* in my terminal: 
* $ bundle gem meals meals (meals is the name of my model class) 
* This command creates a scaffold directory for my new gems.  

bin directory:
  > run file or my executable file:
      where my shebang line is located #!/usr/bin/env ruby  (explicitly telling to execute Ruby)
      require_relative "../lib/environment” 

  
	lib directory:
        
  > environment file. Where I require all my dependencies and classes. 
      this is the connection for my bin directory via run file and lib directory via environment file.

```
require_relative "./meals/version" 

require "pry" 
require "httparty"

require_relative "./api.rb" 
require_relative "./the_meals.rb"
require_relative "./cli.rb"


```
and I created three Classes.

*     Cli.rb or  Cli class my main point of communication with my user

*    Api.rb or   Api class where I consume the api or 
	    get my data url="https://www.themealdb.com/api/json/v1/1/search.php?s

*  Meals.rb => this is the model Class 



