---
layout: post
title:      "Bulletins and Boards "
date:       2020-03-15 23:40:46 -0400
permalink:  my_first_month
---

my Rails Portfolio Project

  welcome to my rails portfolio project summary,  the concept is to build an online bulletin board. 
	bulletin board is a surface(board)  intended for the posting of public messages, for example, to advertise items wanted       or for sale, announce events, or provide information.  
	
after creating Crud actions for class model Board and Bulletin and created a Users sign up and log in, my first question is how can I associate Users and Boards and how can I add Bulletins into the Board??  

looking at my association: `Board belongs_to :user and User has_many :boards` 

```
class Board < ApplicationRecord 
    belongs_to :user
    has_many :bulletins, dependent: :destroy
    has_many :users, through: :bulletins
    validates :title, presence: true 
	end
``` 

```
class Bulletin < ApplicationRecord
    belongs_to :user 
    belongs_to :board 
end
``` 

```
class User < ApplicationRecord 
    has_many :boards
    has_many :bulletins, dependent: :destroy
    has_many :bulletin_boards, through: :bulletins 
 end
```

**connecting users and board** 

`User has_many :boards, through: :bulletins` and `Board has_many users, through: :bulletins` 

in my application controller I define a method called `current_user` this method will allow me to build associations with the user upon creation of a new object.

*app/controllers/applicationcotrller.rb*

```
def current_user
      @current_user ||= User.find_by_id(session[:user_id]) if session[:user_id]
 end
```
  
	Now in my board controller;

*app/controllers/ boardscontroller.rb*


```
def new 
      @board = Board.new
    end 

    def create 
      @board = 
      @board = current_user.boards.build(board_params)

      if @board.save 
        redirect_to board_path(@board)
      else 
        render :new 
      end
    end

```
Now I can create a new board object that is associated with the current user.

**adding bulletins to the board**

in my association, boards has_many  :bulletins and   bulletins belongs_to  : board  

now I can say that` Board` is a parent of` Bulletin`. I can create a nested routes. 

and a link_to for more easier navigation in my application

*config/routes*

  ```
resources :boards do 
    resources :bulletins, shallow: true 
  end   
```

*board index.html.erb*

 `<p> <%= link_to "Create New Bulletins", new_board_bulletin_path(board)%> </p> `  
 
the code below tells us: ` if `board is nested look for board_id in the params `else` create a new bulletins associated with the current_user. 

and add `board_id` to` bulletin_params `
 
*app/controllers/bulletincontroller.rb*
 
```
def new                                                
      if @board = Board.find_by_id(params[:board_id]) if params[:board_id]                             
         @bulletin = @board.bulletins.build 
      else 
        #flash[:message] = "Board does not exist!"
        @bulletin = current_user.bulletins.build 
      end
  end  
```

```
def bulletin_params 
      params.require(:bulletin).permit(:title, :content, :rating, :board_id) 
end 
```

Views 

*view/bulletins/new.html.erb*  

Header for my new form to support the conditional in my new action

`if` nested create nested bulletins for this board `else` create unnested bulletins

```
   <%  if board %>
     <%=  "New Bulletins for #{board.title}" %>
   <% else %>
      <%= "New Bulletin" %>
     <% end %>

```


```
<%= form_for ([@board, @bulletin]) do |f| %>

  <% if !@bulletin.board %> 
	
  <%= f.label :board %>
  <%= f.collection_select :board_id, Board.all, :id, :title %>
	
  <% else %>
  <%= f.hidden_field :board_id %> 
   <% end %>

  <%= f.label :title %>
  <%= f.text_field :title %>
  <%= f.label :content %>
  <%= f.text_field :content %> 
  <%= f.submit %>
<% end %>
```

Setting up my associations and connecting all my models together is the most challenging part of my rails project. 
now I can start adding validations and additional features  in my application. 





















