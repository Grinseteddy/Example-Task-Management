# Exercise 2 - Create A Consumer-Driven API for The Document Management Component

### 1. Create an OpenAPI file called "DocumentManagement.yaml"
- Select OpenAPI
- Give it a meaningful title and a short description
- Define some servers below the servers entry

> ***Tip:***\
_Servers are defined as an array (starting with a hyphen). You can use some phantasy entries in the first place. But
you need to change it later when you know the real URLs. Define URLs for development, test, and production._

[Sample Solution](../API%20Definitions/Synchronous%20APIs/DocumentManagementDesign/DocumentMangementInitialFilling.yaml)

### 2. Create A Walking Skeleton<br>

> ***Tip:***\
_The walking skeleton should contain the necessary paths with a successful response.
The necessary objects should be created empty or with some identifiers._

#### 2.1 Create Some Walking Skeleton Objects
 > ***Tip:***\
 _Objects are created in the schemas section. The schemas section is created below components.
 Your OpenAPI document should have the following structure:_

```yaml
 info:
  #...
 servers:
  #...
 paths:
  #...
 components:
  schemas:
    Document:
      description: #...
      properties:
       #...
    DocumentToBeCreated:
      description: #...
    Reference:
      description: #...
      properties:
        #...
```

- Empty object DocumentToBeCreated
- Document object with a 'self' property as unique identifier
- Reference object with id and uri

>***Tip:***\
_Usually API definition documents can become quite large, and it might be difficult to navigate through them.
Therefore, it is proposed to sort objects alphabetically in the "components: schemas: " area._

#### 2.2 Endpoint to Create a Document

> ***Tip:***\
_The endpoint should contain a description, a request body for the document to be created, and a successful answer. The
successful answer contains as reply a reference to newly created document.
Because the document to be created is a single document, the endpoint should be called in singular._

````yaml
paths:
  /document:
    post:
      description:
        #...
      operationId: createDocument # contains the method name of the implementation
      requestBody:
        #...
      responses:
        200:
          #...
````

> ***Tip:***\
_Successful responses need at least a description. The object delivered back can be entered as content with the format 
e.g., application/json. Responses can be defined in the area "responses" below components and can be referenced using
'$ref:' expression.\
>The request body can be defined inside the endpoint or it can be defined below "components" and "requestBodies" 
as reference._

````yaml
components:
  requestBodies:
    DocumentToCreated:
      description: #...
      content:
        application/json:
          schema:
            $ref: #...
    
  responses:
    Reference:
  schemas:
      #...
````

- Create an endpoint which can be used to create a document with a request body containing the document to be created
and a successful response

#### 2.3 Endpoint To Get and Change A Document By ID

>***Tip:***:\
_Define a parameter where the ID can be given over. You can define the parameter in the "parameters" section below
components. The parameter has to have a name and an "in:", where is defined, how to give over the parameter. It can
be query or as in our case as path variable._

````yaml
components:
  parameters:
    DocumentId:
      name: id
      in: path
      #...
````

- Define an endpoint to retrieve a document by its ID (get)
- Define an endpoint to update a document by its ID (put)




