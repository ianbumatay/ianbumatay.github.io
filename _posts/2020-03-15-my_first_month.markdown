---
layout: post
title:      "Bulletins and Boards ####my Rails Portfolio Project "
date:       2020-03-15 23:40:46 -0400
permalink:  my_first_month
---


  welcome to my rails portfolio project summary, 	I call it free board the concept is to build an online bulletin board. 
	bulletin board is  is a surface intended for the posting of public messages, for example, to advertise items wanted or for     sale, announce events, or provide information. 
	
	
	#### Generate migration for my class models User, Board, Bulletins 
	
	rails generate <name of generator> <options> --no-test-framework 
	
	--no-test-framework is a flag that tells the generator not to create any tests for the newly-generated models, controllers, etc.



#### setting up associations 

```
class User < ApplicationRecord 
    has_many :boards
    has_many :bulletins, dependent: :destroy
    has_many :bulletin_boards, through: :bulletins 
    has_secure_password 
    validates :username, :email, presence: true, uniqueness: true  
end
``` 
```
class Bulletin < ApplicationRecord
    belongs_to :user 
    belongs_to :board 
 end
```
```
class Board < ApplicationRecord 
    belongs_to :user
    has_many :bulletins, dependent: :destroy
    has_many :users, through: :bulletins
    validates :title, presence: true 
end
```



