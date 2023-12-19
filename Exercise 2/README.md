# Exercise 2 - Create a Consumer-Driven API for the Document Management Component

### 1. Create an OpenAPI file named `DocumentManagement.yaml`
- Select OpenAPI
- Give it a meaningful title and a short description
- Define some servers below the server entry

> ***Tip:***\
_Servers are defined as an array (starting with a hyphen). You can use some phantasy entries in the first place. But
you need to change it later when you know the real URLs. Define URLs for development, test, and production._

[Sample Solution](../API%20Definitions/Synchronous%20APIs/DocumentManagementDesign/DocumentMangementInitialFilling.yaml)

### 2. Create a Walking Skeleton

> ***Tip:***\
_The walking skeleton should contain the necessary paths with a successful response.
The necessary objects should be created empty or with some identifiers._

#### 2.1 Create Some Walking Skeleton Objects
 > ***Tip:***\
 _Objects are created in the schemas section. The schemas section is created below components.
 Your OpenAPI document should have the following structure:_

- Empty object DocumentToBeCreated
- Document object with a 'self' property as unique identifier
- Reference object with `id` and `uri`

>***Tip:***\
_When you define string properties, you should limit the implementation corridor.
So, it would be a good idea to limit the size of the string to a minimal length and a maximal length.
Furthermore, you can give a string a certain format, e.g., `email` or `uuid`.
([OpenAPI specification: string](https://swagger.io/docs/specification/data-models/data-types/#string))._


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
      type: object
      required:
        - self
      properties:
        self:
          description: #...
          type: string
          format: uuid
          example: # uuid example
    DocumentToBeCreated:
      description: #...
      type: object
      required:
        - title
      properties:
        title:
          description: #...
          type: string
          minLength: # some number >1
          maxLength: # some number > minLength
          example: # example
    Reference:
      description: #...
      type: object
      required:
        - id
        - url
      properties:
        id:
          description: #...
          type: string
          format: uuid
          example: # uuid example
        url:
          description: #...
          type: string
          format: uri
          example: # url example
```

>***Tip:***\
_Usually API definition documents can become quite large, and it might be difficult to navigate through them.
Therefore, it is proposed to sort objects alphabetically in the "components: schemas: " area._

#### 2.2 Endpoint to Create a Document

> ***Tip:***\
_The endpoint should contain a description, a request body for the document to be created, and a successful answer. The
successful answer contains as a response a reference to a newly created document.
Because the document to be created is a single document, the endpoint should be named in the singular._

- Create an endpoint that can be used to create a document with a request body containing the document to be created
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
_Successful responses need at least a description. The object delivered back can be entered as content with the format,
e.g., `application/json`. Responses can be defined in the area `responses` below components and can be referenced using
`$ref:` expression.\
> The request body can be defined inside the endpoint or it can be defined below "components" and "requestBodies"
as reference._

````yaml
components:
  requestBodies:
    DocumentToBeCreated:
      description: #...
      content:
        application/json:
          schema:
            $ref: #...
  schemas:
      #...
````



#### 2.3 Endpoint To Get and Change a Document By ID

- Define an endpoint to retrieve a document by its ID (get)
- Define an endpoint to update a document by its ID (put)

>***Tip:***\
_Define a parameter where the ID can be given.
You can define the parameter in the `parameters` section below `components`.
The parameter has to have a name and an "in:", where it is defined, how to give over the parameter.
It can be "query" or as in our case it can be a "path" variable._

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
     requestBodies:
       #...
      DocumentToBeUpdated:
        # Define a request body for the update using the Document object
     responses:
      200:
       description: #...
       content:
        application/json:
         schema:
          $ref: '#...'
````

#### 2.4 OPTIONAL Delete by ID

>***Tip:***\
_The "delete" endpoint gets a parameter and delivers nothing back.
But keep in mind that the successful response 200 needs a description._

- Enhance the endpoint `/document/{id}:` by a delete method:

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
Usually, those lists can be used to find the correct document, but we don't have such a case in our domain stories.
We use it here, only to show, how to handle such a list.
Lists are modeled as arrays._

- Create a documents endpoint, which gives back a list of documents (without any filter):

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

# Excercise 3 - Define Properties for the Objects

### 3.1 Define Properties for DocumentToBeCreated

- Fill the object DocumentToBeCreated with
    - Title
    - File Name
    - Document
    - Created By

  Mark the necessary attributes in the required section.

>***Tip:***\
>_Each property must have a description_

> ***Tip:***\
_Title and filename can be strings. Please define for both at least a minimal length and a maximal length.
Check [here](https://swagger.io/docs/specification/data-models/data-types/#string)
how to define minimal length and maximal length for strings in OpenAPI.\
The document itself needs to be binary - check [here](https://swagger.io/docs/specification/data-models/data-types/#string)
how to define binaries in OpenAPI_

>***Tip:***\
_Sometimes it might be helpful to restrict the strings by regular expression. Check if the regular expression
`^\w+.(docx|pdf|pptx|exec)$` might be helpful to restrict the file formats only to Word, PDF, or PPTX documents._

>***Tip:***\
_'Created by' should be some kind of user of the system. Because we define the Task Management System and the
Document Management system only out of the consumer perspective, we want only to exchange the user as a reference._

````yaml
components:
#...
  schemas:
      #...
      DocumentToBeCreated:
        description: #...
        operationId: #...
        type: object
        required:
          - title
          #...
        properties:
          title:
            description: #...
            type: string
            minLength: #...
            maxLength: #...
            pattern: #...
            example: #...
          fileName:
            description: #...
            type: string
            pattern: #...
            example: #...
          document:
            description: #...
            type:
            format: binary
            # here without example, because that would be too large
````

### 3.2 Enhance Document Object

- Fill the Document object with the same data as DocumentToBeCreated
- Fill the Document object additionally with
    - `createdAt`
    - `updatedBy`
    - `updatedAt`

  Mark the necessary properties in the required section.

>***Tip:***\
_OpenAPI provides mechanisms to model inheritance and polymorphism even for API objects.
[Check](https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism/) the possibilities of oneOf,
allOf, etc. To use all things of one object in another object, you can use 'allOf'_

>***Tip:***\
_Date and Date-Time are modeled in OpenAPI as strings. You need to define the according
[format](https://swagger.io/docs/specification/data-models/data-types/#string) for dates._

````yaml
components:
#...
  schemas:
  #...
    Document:
      description: #...
      type: object
      required:
        - self
        #...
      allOf:
        - $ref: '#/components/schemas/DocumentToBeCreated'
      properties:
        self:
          #...
        createdAt:
          description: #...
          type: string
          format: date
          example: #...
        updatedBy:
          $ref: '#...'
        updatedAt:
          description: #...
          type: string
          format: date
          example: #...
````

### 3.3 OPTIONAL Define A Query for The Document List

>***Tip:***\
_To define a query, the parameters can be defined in the parameters section. Parameters are defined with name and in._

- Define query parameters for the `/documents` endpoint using `DocumentName` and `Title`.

````yaml
path:
#...
  /documents:
    get:
      #...
        parameters:
          # use here the defined parameters
#...
components:
#...
  parameters:
    #...
    DocumentName:
      name: # name starts with a small letter
      in: query
      required: false
      description: #...
      schema:
        type: #...
        pattern: # use the name pattern as defined in DocumentToBeCreated
        example: #...
    Title:
      name: # ...
      in: query
      required: false
      description: #...
      schema:
        type: #...
        pattern: # use the same pattern as for the title in the DocumentToBeCreated
        example: #...
````
