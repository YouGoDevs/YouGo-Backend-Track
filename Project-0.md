# Project 0: PICS OR IT DIDN’T HAPPEN

> Overview: In this project, you’ll be building a (mostly) backend API that allows users to upload an image and either have it stored or have it manipulated in some way and returned.

Notes:
- This requirements doc will also point you in the right direction of some design decisions to consider, but it won’t cover everything. Part of being a developer is working with ambiguity and making the best decision possible with the available information, making reasonable assumptions of how the service may grow in the future.
- There will be brownie points for this (and any) project if you choose to do it in Golang instead of making me read Node.js 😅. But prioritizing getting the job done over learning something new is also a reasonable decision.

## Part 0: The Agreement
For this part, the client wants to send an image to an HTTP(S) endpoint, specify some manipulation, and receive the manipulated image back as a response. The manipulations that need to be supported right now include:
- Image resizing
- Grayscale
- Transformations (rotate, inversion).
- At least two methods supported by the image processing library you choose. 

Your first task will be to make your API specification for the service. This spec will be shared with the client. Technically, as long as the client knows how to interact with your service, any method you choose to convey that information will work. You could easily have the spec in a README, for example. But I want you to learn how industries do this so we’ll aim higher. You will document your service more officially, according to the OpenAPI specification version 3. This type of specification is known commonly as a “swagger spec”. I’ll allow you to do your research, read and become familiar with it ([OpenAPI Specification & Swagger Tools](https://swagger.io/resources/open-api/) is a great site to start). But it essentially allows you to specify all aspects of the service using YAML or JSON. [editor.swagger.io](https://editor.swagger.io/) is a great editor to compose your spec with real-time feedback and visualization. It starts you off with an excellent example spec (hint: one of the endpoints in the spec relates to image upload).  
The handy thing about having a swagger spec is that it will generate the client and server-side code compliant with the spec. Right now, we care about the server-side stubs, but in a future part, you’ll spin up a front-end to interact with the API.

### Some decisions you’ll need to make in this step:
- What image processing client you’ll leverage. [Sharp](https://github.com/lovell/sharp) appears to be the most popular, but there are also the likes of [Jimp](https://github.com/oliver-moran/jimp).
- How will you architect your API to be ergonomic and organized for the user? Throughout this project, I expect proper, conventional use of [HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) and accurate response [codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) (i.e., using 200/201/202/204 when appropriate, not just 200 for everything). 
- You’ll have to decide if you want an endpoint for each type of manipulation vs. one endpoint for all manipulations vs. something else. How will users provide details? Will you use path parameters, query parameters, or accept a JSON body?
- How will users upload images, and how will you return them? Multipart/form-data or base64 encoded string?
- Where will you host this service? I can’t test this if it only lives on localhost. Pick something with a generous free tier to host APIs and some storage.

> TIP: If you haven’t used Postman in the past, it’s an excellent resource for testing APIs.

### At the end of Part 0, you should deliver:
- Github repo for the project, containing:
  - [ ] The swagger Spec
  - [ ] The server-side generated API stubs
  - [ ] Your node.js logic that hooks into the stubs
  - [ ] README about the project
  - [ ] Another markdown file on the design decisions you’ve made so far, defending your choice with pros/cons (definitely answer all the questions I posed above, plus whatever else you had to decide) 
- The hosted API
___

## Part 1: The Horizontals
So you've created the MVP (minimum viable product) for your API and shared it with some friends. However, they keep comparing it to what Google Photos can do - where you can do some filters, but it also allows users to store images and upload/download/manipulate them at will. You agree that image storage should be the next logical step for your API (Hopefully, you picked a service host provider that integrates nicely with a storage product with a generous free tier).

You will create a few more endpoints/options for your API service for this task. Users should be able to 
- Upload an image to be stored, 
- Get a list of images stored (the image name/id, not the actual image), 
- Download an image by name/id, 
- Perform a supported manipulation on a stored image (specified by image name/id) and return the manipulated image. Brownie points if you allow the user to save an uploaded copy of the manipulated image.

Of course, since you now have a user base, you'll also need a database and a way to authenticate users' requests. In this task, you'll also have a user sign-up endpoint. For now, you'll only support username+password authentication. Feel free to enforce whatever validations you'd like (i.e., all usernames must be unique, a minimum length for passwords, etc.). You can also have the sign-up API optionally collect useful personal information like name, DOB, location. Before storing the username and password in a DB, you should first salt and hash it. All APIs (including those from the previous task) will now be protected routes (requiring auth). Since we're making a REST API service, we won't have the idea of a user session. Instead, the user will pass authentication headers with each request. The header should be in a form where the key is `auth`, and the value is a base64 encoded `username;password`. 
> Note: This is **not** a sufficient or advised approach for authenticating. This approach is structured explicitly as a teaching goal to give some experience with salting, hashing, encryption, and encoding. Later on, we will implement a better auth story.

### Questions to consider:
- Does your existing API design structure support this expansion in a smooth way that makes sense to a consumer of the API?
- Would it be smoother to have one upload/download/delete endpoint and use the correct HTTP method to differentiate?
- What hashing function/library should you use? Do efficiency considerations of the hashing algorithm change, given you'll have to perform encryption on a per request basis?
- What database type meets your needs now and potentially in the future? How do you design/structure data you're hoping to store?
- Does it make sense to collect some personal info from the client at this point? What data is necessary? What data is useful?
- Do you need to limit the total available storage of a given user? 

### At the end of part 1, you should deliver:
- [ ] The new endpoints specified above enable users to upload, download, store, and manipulate images.
- [ ] A user login endpoint
- [ ] A database to hold details (plus schema, if necessary)
- [ ] Storage solution to host images

## Part 2: The Makeover
With part 1 complete, you want to share your product more widely. The problem is that most people don't want to call an API directly. Most have never heard of Postman. To get the opinions of a more general audience, in this step, you'll create a simple front-end client.  
This project isn't front-end focused, so I expect a clean, minimal design. I don't particularly care what framework or front-end stack you use. The pages/screens expected:
- [optional] Landing page
- Login page
- User's Home page displaying their uploaded images
- Allow the user should click on an image thumbnail and display the full-size image.
- Image edit page where the user can see the result of applying the various transformations implemented thus far and save a copy of the transformed image.

To be clear, this should be a "dumb" client that simply calls your existing backend APIs, such as auth and image transformations. DO NOT re-implement functionality that already exists.

### At the end of this part, you should deliver:
- [ ] A hosted, front-end client
- [ ] Updated README on how to interact with your app.