---
layout: post
title:      "Putting All The Pieces Together"
date:       2020-12-20 21:14:48 -0500
permalink:  my_js_project_cheat_sheet
---

Understanding how we put the pieces together gives me solid uderstanding and preparedness in my upcoming javascript project.

First thing first is to assign my backend ulr to a class variable.

```
 BACKEND_URL =  'http://localhost:3000/posts'
``` 

I  wanted to grab the  <form> by querying the Id => *document.getElementById("form") *	

```
     <form id="form">
        <label for=" ">:Content</label>
        <input type="text" id="user-input">
        <input type="submit" >
      </form>
			
			
const form = document.getElementById("form") 		

```


Adding an eventlistener and passing a callback function called submitForm.

```
form.addEventListener("submit", submitForm) 
```

The SubmitForm Function  is a function responsible for grabbing user input and submiting the form in the database.

* preventDefault() =>

* Getting the Users Input value. => .value

* option => 

* fetch(BACKEND_URL, option) =>
* 

```

function submitForm(){

    event.preventDefault()
		
    const input = document.getElementById('user-input').value

    options = {
        method: 'POST', 
        headers: {
            'Content-type': 'application/json', 
            'Accept': 'application/json'
        }, 
        body: JSON.stringify({post: {content: input}})
    }

    fetch(listUrl, options)
    .then(res => res.json())
    .then(postObj => renderPost(postObj.data))
} 

```

*renderPost function *

Responsible for creating the HTML elements and showing the data in the browser. 
Data that comes from the user input and it gets passed back and fort

```
function renderPost(post){
    const div = document.getElementById('postContainer')
    const pTag = document.createElement('p')
    pTag.innerText = post.attributes.name
    div.appendChild(pTag)
} 
```


fetchPost function is responsible  for showing all the post that have been created. 
from the backend

we have to invoke the function for it to render all post.

```
function fetchPost(){
    fetch(BACKEND_URL)
    .then(res => res.json())
    .then(posts => posts.data.forEach(renderPost))
}

fetchPost()


```



