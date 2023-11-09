# Excercise 3 - Define Properties for the Objects

### 3.1 Define Properties for DocumentToBeCreated

- Fill the object DocumentToBeCreated with
  - Title
  - File Name
  - Document
  - Created By\

  Mark the necessary attributes in the required section.

>***Tip:***\
>_Each property must have
>- a desription
_

> ***Tip:***\
_Title and File Name can be strings. Please define for both at least a minimal length and a maximal length.
Check [here](https://swagger.io/docs/specification/data-models/data-types/#string)
how to define minimal length and maximal length for strings in OpenAPI.\
The document itself needs to be binary - check [here](https://swagger.io/docs/specification/data-models/data-types/#string)
how to define binaries in OpenAPI_

>***Tip:***\
_Sometimes it might be helpful to restrict the strings by regular expression. Check if the regular expression
'^\w+.(docx|pdf|pptx|exec)$' might be helpful to restrict the file formats only to Word, PDF, or PPTX documents._

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
  - createdAt
  - updatedBy
  - updatedAt\
  
  Mark the necssary properties in the required section.

>***Tip:***\
_OpenAPI provides mechanisms to model inheritance and polymorphism even for API objects.
[Check](https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism/) the possibilities of oneOf,
allOf, etc. To use all things of one object in another object, you can use 'allOf'_

>***Tip:***\
_Date and Date-Time are modeled in OpenAPI as string. You need to define the according

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
