**PUT** replaces the resource at the known url if it already exists, so sending the same request twice has no effect. 
In other words, calls to PUT are idempotent. PUT is for creating or replacing a resource at a URL known by the client. URI in a 
PUT request identifies the entity enclosed with the request and the server MUST NOT attempt to apply the request to some other resource.

**POST** creates a child resource, so POST to /items creates a resources that lives under the /items resource. Eg. /items/1. 
Sending the same post packet twice will create two resources. The URI in a POST request identifies the resource that will handle 
the enclosed entity. That resource might be a data-accepting process, a gateway to some other protocol, or a separate entity that 
accepts annotations.

When you use POST you are always refering to a collection, so whenever you say:
**POST /users**
you are posting a new user to the users collection.

If you go on and try something like this:
**POST /users/john**
it will work, but semantically you are saying that you want to add a resource to the john collection under the users collection.


Once you are using PUT you are refering to a resource or single item, possibly inside a collection. So when you say:
**PUT /users/john**
you are telling to the server update, or create if it doesn't exist, the john resource under the users collection.

**PATCH** to a URL updates part of the resource at that client defined URL.
