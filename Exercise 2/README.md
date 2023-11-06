# Exercise 2 - Create a Consumer-Driven API for The Document Management Component

#### 1. Create an OpenAPI file called "DocumentManagement.yaml"
1.1 Select OpenAPI\
1.2 Give it a meaningful title and a short description
1.3. Define some servers below the servers entry.

***Tip:***\
_Servers are defined as an array (starting with a hyphen). You can use some phantasy entries in the first place. But
you need to change it later when you know the real URLs. Define URLs for development, test, and production._

   [Sample Solution](../API%20Definitions/Synchronous%20APIs/DocumentManagementDesign/DocumentMangementInitialFilling.yaml)

2. Create a Walking Skeleton<br>

***Tip:***\
_The walking skeleton should contain the necessary paths with a successful response.
The necessary objects should be created almost empty or with some identifiers._

#### 2.1 Create some Walking Skeleton objects
 ***Tip:***\
 _Objects are created in the schemas section. The schemas section is created below components.
 Your OpenAPI document should have the following structure on the first level:_

```yaml
 info
 servers
 paths
 components
```

##### 2.1.1 Empty object DocumentToBeCreated
##### 2.1.2 Document object with a 'self' property as unique identifier
##### 2.1.3 Reference object with id and uri

      