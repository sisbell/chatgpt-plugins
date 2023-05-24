**Question**: Can GPT discover new resources based on links in a response? This tests a basic REST principle of 
a client understanding hyperlinks.

This experiment allows a user to request event data for conferences. Each event has a link where more detail can
be found. If ChatGPT makes a call to that link, then it understands how to use hypermedia links. 
I give it a definition of links in the OpenAPI Spec so that it understands the concept. 
I also give instruction in the prompt on how a link should be used.

**Prompt Used**:
A plugin that allows the user to search for event conferences. The events response will provide a link event that you need to call to
get the event details. Call that and return the info to user.

**Definition of a link**
```yaml
components:
  schemas:
    Event:
      type: object
      properties:
        id:
          type: string
          example: "1"
        eventName:
          type: string
          example: "Conference on Artificial Intelligence"
        links:
          type: object
          properties:
            events:
              type: string
              example: "https://localhost:5003/event/1"
```

**Chat Test**
<img width="828" alt="hateoas" src="https://github.com/sisbell/chatgpt-plugins/assets/64116/5b11987f-3677-4c6e-9cda-1784bf2036a4">

We see that ChatGPT attempts to make 3 calls to each event id to get more details. It does understand the concept
of hyperlinks based on simple instructions. 

However, since these specific event links ere not defined in the schema, 
ChatGPT blocks the request. No request ever reaches the servers. 

**Conclusion**
This experiment shows that ChatGPT has understanding of hyperlinks but has 
been restricted to only make calls to what is specified in the OpenAPI Spec. 
This limits the plugin to a more traditional remote procedure call. It is 
unable to crawl the web and to discover more information.

