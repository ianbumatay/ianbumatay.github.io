---
layout: post
title:      "Putting it all Together "
date:       2020-12-20 21:14:48 -0500
permalink:  my_js_project_cheat_sheet
---

first thing first is to setup backend url 

```
 BACKEND_URL =  'http://localhost:3000/posts'
``` 

Grabbing the <form> 

```
<form id="form">
        <label for=" ">:Content</label>
        <input type="text" id="user-input">
        <input type="submit" >
      </form>
			
			
const form = document.getElementById("form") 		

```


Adding Events

```
form.addEventListener("submit", submitForm) 
```

The Function SubmitForm
Submitting The form with preventDefault() method. 
Getting the Users Input value. by adding .value
This fuction is responsible for getting the data and submmiting it to the backend.
and converts it to jason object.

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


renderPost function 
is responsible for creating the HTML elements and showing the data in the browser. 
the data that come from the user input.

function renderPost(post){
    const div = document.getElementById('postContainer')
    const pTag = document.createElement('p')
    pTag.innerText = post.attributes.name
    div.appendChild(pTag)
} 


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



