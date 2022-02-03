# Project 0: PICS OR IT DIDN’T HAPPEN

> Overview: In this project, you’ll be building a (mostly) backend API that allows users to upload an image and either have it stored or have it manipulated in some way and returned.

Notes:
- This requirements doc will also point you in the right direction of some design decisions to consider, but it won’t cover everything. Part of being a developer is working with ambiguity and making the best decision possible with the available information, making reasonable assumptions of how the service may grow in the future.
- There will be brownie points for this (and any) project if you choose to do it in Golang instead of making me read Node.js 😅. But prioritizing getting the job done over learning something new is also a reasonable decision.

## Part 0
For this part, the client wants to send an image to an HTTP(S) endpoint, specify some manipulation, and receive the manipulated image back as a response. The manipulations that need to be supported right now include:
- Image resizing
- Grayscale
- Transformations (rotate, inversion).
- At least two methods supported by the image processing library you choose. 

Your first task will be to make your API specification for the service. This spec will be shared with the client. Technically, as long as the client knows how to interact with your service, any method you choose to convey that information will work. You could simply have the spec in a README, for example. But I want you to learn how industries do this so we’ll aim higher. You will document your service more officially, according to the OpenAPI specification version 3. This type of specification is known commonly as a “swagger spec”. I’ll allow you to do your research, read and become familiar with it ([OpenAPI Specification & Swagger Tools](https://swagger.io/resources/open-api/) is a great site to start). But it essentially allows you to specify all aspects of the service using YAML or JSON. [editor.swagger.io](https://editor.swagger.io/) is a great editor to compose your spec with real-time feedback and visualization. It starts you off with an excellent example spec (hint: one of the endpoints in the spec relates to image upload).  
The handy thing about having a swagger spec is that it will generate the client and server-side code compliant with the spec. Right now, we care about the server-side stubs, but in a future part, you’ll spin up a front-end to interact with the API.

### Some decisions you’ll need to make in this step:
- What image processing client you’ll leverage. [Sharp](https://github.com/lovell/sharp) appears to be the most popular, but there are also the likes of [Jimp](https://github.com/oliver-moran/jimp).
- How will you architect your API to be ergonomic and organized for the user? Throughout this project, I expect proper, conventional use of [HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) and accurate response [codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) (i.e., using 200/201/202/204 when appropriate, not just 200 for everything). 
- You’ll have to decide if you want an endpoint for each type of manipulation vs. one endpoint for all manipulations vs. something else. How will users provide details? Will you use path parameters, query parameters, or accept a JSON body?
- How will users upload images, and how will you return them? Multipart/form-data or base64 encoded string?
- Where will you host this service? I can’t test this if it only lives on localhost. Pick something with a generous free tier to host APIs and some storage.

> TIP: If you haven’t used Postman in the past, it’s an excellent resource for testing APIs.

### At the end of Part 0, you should deliver:
Github repo for the project, containing:
- [ ] The swagger Spec
- [ ] The server-side generated API stubs
- [ ] Your node.js logic that hooks into the stubs
- [ ] README about the project
- [ ] Another markdown file on the design decisions you’ve made so far, defending your choice with pros/cons (definitely answer all the questions I posed above, plus whatever else you had to decide) 
- [ ] The hosted API
