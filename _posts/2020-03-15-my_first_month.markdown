---
layout: post
title:      "Bulletins and Boards "
date:       2020-03-15 23:40:46 -0400
permalink:  my_first_month
---

my Rails Portfolio Project Key Concepts

  welcome to my rails portfolio project summary, 	I call it free board the concept is to build an online bulletin board. 
	bulletin board is a surface(board)  intended for the posting of public messages, for example, to advertise items wanted       or for sale, announce events, or provide information.  
	

after creating Crud action for my Board and Bulletins, my first question is how can I add bulletins into the board?? 

in my association, boards has_many  :bulletins and   bulletins belongs_to  : board  

now I can say that` Board` is a parent to` Bulletin`

 I can create a nested routes. and a link_to  

*config/routes*

  ```
resources :boards do 
    resources :bulletins, shallow: true 
  end   
```

*board index.html.erb*

 <p> <%= link_to "Create New Bulletins", new_board_bulletin_path(board)%> </p>   
 
 adding :board_id to bulletin params and finding a nested board and create bulletins for that board  or creating a new bulletins.
 
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

```
   <%  if board %>
     <%=  "New Bulletins for #{board.title}" %>
   <% else %>
      <%= "New Bulletin" %>
     <% end %>

```
if nested create nested bulletins for this board else create unnested bulletins

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

























