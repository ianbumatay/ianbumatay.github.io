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

* preventDefault() => Prevent default action of the browser. 
   example: Clicking on a "Submit" button, prevent it from submitting a form(GET)

* Getting the Users Input value. => .value property to grab the input value.

* configobject => takes three core components. 

**Method :** POST
	
 ** Headers** :  "Content-Type" :tells the destination server what type of data we're sending.  "Accept" : tell the server what       data format we accept in return. 
 
** Body:**  "data goes here" JSON.stringify() to Convert Objects to Strings

  fetch(BACKEND_URL, object) =  construct a POST request :   atake two arguments the url and an object ={}.


```

function submitForm(){

    event.preventDefault()
		
    const input = document.getElementById('user-input').value

    configobject = {
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

renderPost function 

is a function Responsible for creating the HTML elements and showing the data in the browser. 
Data that comes from the user input and it gets passed backend to frontend.

```
function renderPost(post){
    const div = document.getElementById('postContainer')
    const pTag = document.createElement('p')
    pTag.innerText = post.attributes.name
    div.appendChild(pTag)
} 
```


fetchPost function is a function responsible  for fetching all data in the sever and showing all the post that have been created. from the backend

we have to invoke the function for it to render all post. => fetchPost()

```
function fetchPost(){
    fetch(BACKEND_URL)
    .then(res => res.json())
    .then(posts => posts.data.forEach(renderPost))
}

fetchPost() <= we have to invoke the function for it to render all post. 


```



