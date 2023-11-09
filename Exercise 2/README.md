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

- Empty object DocumentToBeCreated
- Document object with a 'self' property as unique identifier
- Reference object with id and uri


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

>***Tip:***\
_Usually API definition documents can become quite large, and it might be difficult to navigate through them.
Therefore, it is proposed to sort objects alphabetically in the "components: schemas: " area._

#### 2.2 Endpoint to Create a Document

> ***Tip:***\
_The endpoint should contain a description, a request body for the document to be created, and a successful answer. The
successful answer contains as reply a reference to newly created document.
Because the document to be created is a single document, the endpoint should be called in singular._

- Create an endpoint which can be used to create a document with a request body containing the document to be created
  and a successful response

````yaml
paths:
  /document:
    post:
      description:
        #...
      operationId: createDocument # contains the method name of the implementation
      requestBody:
        $ref: '#/components/DocumentToBeCreated'
      responses:
        200:
          description: Successful operation
          content:
            application/json:
              # Reference to the "Reference" object          
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
  schemas:
      #...
````



#### 2.3 Endpoint To Get and Change A Document By ID

>***Tip:***\
_Define a parameter where the ID can be given.
You can define the parameter in the "parameters" section below components.
The parameter has to have a name and an "in:", where is defined, how to give over the parameter. 
It can be "query" or as in our case as "path" variable._

````yaml
components:
  parameters:
    DocumentId:
      name: id
      in: path
      schema:
        type: ...
````

````yaml
paths:
  /document/{id}:
    get:
      description: #...
      operationId: #...
      parameters:
       - $ref: '#...'
      responses:
        200:
          description: #...
          content:
            application/json:
              schema:
                $ref: '#...'
    put:
     description: #...
     operationId: #...
     parameters:
      - $ref: '#...'
     responses:
      200:
       description: #...
       content:
        application/json:
         schema:
          $ref: '#...'
````

- Define an endpoint to retrieve a document by its ID (get)
- Define an endpoint to update a document by its ID (put)

#### 2.4 OPTIONAL Delete by ID

>***Tip:***\
_The "delete" endpoint gets a parameter and delivers nothing back.
But have in mind that the successful response 200 needs a description._

- Enhance the endpoint "/document/{id}:" by a delete method

````yaml
paths:
  /document/{id}:
    delete:
      description: #...
      operationId: #...
      parameters:
        #...
      responses:
        200:
````

#### 2.5 OPTIONAL Get a Documents List

>***Tip:***\
_The document list below the "/documents" endpoint is optional.
Usually those lists can be used to find the correct document, but we don't have such a case in our domain stories.
WE use it here, only to show, how to handle such a list.
Lists are modeled as arrays._

- Create a documents endpoint, which gives back a list of documents (without any filter)

````yaml
paths:
 /documents:
  get:
   description: #...
   operationId: #...
   responses:
    200:
      description: #...
      content:
        application/json:
          schema:
            type: array
            items:
             $ref: '#...'
````

[Sample Solution](../API%20Definitions/Synchronous%20APIs/DocumentManagementDesign/DocumentMangementWalkingSkeleton.yaml)