# Requirements for EZGas

Authors: 
- Gabriele Durantini : s276956
- Antonin Louis Leon Poche : s275011
- Alessandro Pisani : s269274
- Huseyin Cagri Karakus : s279122

# Contents
- [Abstract](#abstract)
- [Stakeholders](#stakeholders)
- [Context Diagram and interfaces](#context-diagram-and-interfaces)
  + [Context Diagram](#context-diagram)
  + [Interfaces](#interfaces) 
  
- [Requirements for EZgaz](#requirements-for-ezgaz)
- [Contents](#contents)
- [Abstract](#abstract)
- [Stakeholders](#stakeholders)
- [Context Diagram and interfaces](#context-diagram-and-interfaces)
  - [Context Diagram](#context-diagram)
  - [Interfaces](#interfaces)
- [Stories and personas](#stories-and-personas)
- [Functional and non functional requirements](#functional-and-non-functional-requirements)
  - [Functional Requirements](#functional-requirements)
  - [Non Functional Requirements](#non-functional-requirements)
- [Use case diagram and use cases](#use-case-diagram-and-use-cases)
  - [Use case diagram](#use-case-diagram)
  - [Use Cases](#use-cases)
    - [Use case 1, UC1 - FR4.1 Add a gas station](#use-case-1-uc1---fr41-add-a-gas-station)
    - [Use case 2, UC2 - FR4.2 Modify a gas station](#use-case-2-uc2---fr42-modify-a-gas-station)
    - [Use case 3, UC3 - FR4.3 Delete a gas station](#use-case-3-uc3---fr43-delete-a-gas-station)
    - [Use case 4, UC4 - FR5 Update a price](#use-case-4-uc4---fr5-update-a-price)
    - [Use case 5, UC5 - FR7 Register](#use-case-5-uc5---fr7-register)
    - [Use case 6, UC6 - FR3 Search information](#use-case-6-uc6---fr3-search-information)
    - [Use case 7, UC7 - FR6 Login](#use-case-7-uc7---fr6-login)
    - [Use case 8, UC8 - FR8 Users Management](#use-case-8-uc8---fr8-users-management)
    - [Use case 9, UC10 - FR9 Request management](#use-case-9-uc10---fr9-request-management)
- [Relevant scenarios](#relevant-scenarios)
  - [Scenario 1](#scenario-1)
  - [Scenario 2](#scenario-2)
  - [Scenario 2](#scenario-2-1)
  - [Scenario 4](#scenario-4)
  - [Scenario 5](#scenario-5)
  - [Scenario 6](#scenario-6)
  - [Scenario 7](#scenario-7)
  - [Scenario 8](#scenario-8)
  - [Scenario 9](#scenario-9)
- [Glossary](#glossary)



# Abstract

EZgas is a crowdsourcing application that allows users to find the nearest Gas stations and consult their fuel prices.

Users can use the application even if they're not registrered.
In this case, they can only search information about Gas stations (address, prices, fuel types). If a user decides to register, he will have the possibility to update Gas stations fuel prices and to add, update or delete Gas stations.
And should do it for the application to work. 

An administrator manages registered users reliability and  their accounts. The administrator also verify the truthfulness of registered users requests (add new Gas stations, delete Gas stations, update Gas stations), while an algorithm manages the update of Gas stations fuel prices.
If a registered user inserts wrong information, his reliability will decrease and his requests will not be accepted.



# Stakeholders

| Stakeholder name  | Description |   
| ----------------- |:-----------:|   
| Unregistered User   | Uses the application to search information about Gas stations (address, prices, fuel types) |   
| Registrered User | Uses the application to search information about Gas stations (address, prices, fuel types). He can also add, update or delete Gas stations, and update their fuel prices  |
| Administrator         | Maintain the application, manage registered user requests and account | 
 


# Context Diagram and interfaces

## Context Diagram

```plantuml
left to right direction
actor Users as u
actor Administrator as a
u -- (EZgas)
a -- (EZgas)
```

## Interfaces
| Actor | Logical Interface | Physical Interface  |   
| ------------- |:-------------:| -----:|   
| Users | GUI | Computer |   
| Administrator | GUI |Screen, keyboard|



# Stories and personas

Bobby needs to refuel and he is not close to his usual Gas station, therefore he looks for a Gas station.

Donald also needs to refuel, but he is short on money and he would like to find the nearest Gas station with the cheapest fuel price.

The developer wish to make a useful crowdsourcing application. He believes in the user donations to be paid and eventually in the future he will insert some advertisements.

John wants to get information about Gas stations but he knows that he can find reliable information only if many people participate and update fuel prices and Gas stations. Therfore John participates, be John.



# Functional and non functional requirements

## Functional Requirements

| ID    | Description  |    
| ------------- |:-------------:|       
| FR1   | Record Gas stations |
| FR2   | Record fuel prices in a Gas station |
| FR3   | Search Gas station |
| FR3.1 | Find nearest Gas stations |
| FR3.2 | Order Gas stations by price |
| FR3.3 | Search a specific fuel type |
| FR4   | Manage Gas stations |
| FR4.1 | Manage addition of a Gas station |
| FR4.2 | Manage updating of a Gas station |
| FR4.3 | Manage deletion of a Gas station |
| FR5   | Manage Gas stations fuel prices updating |
| FR6   | Manage users (administrator) |
| FR7   | Manage users registration |
| FR8   | Manage users login |
| FR9   | Manage users reliability |
| FR10  | Manage Gas station modification requests (administrator) |

## Non Functional Requirements

| ID     | Type        | Description  | Refers to |          
| ------------- |:-------------:| :-----:| -----:|         
|  NFR1  | Usability   | Application should be easy to understand and to use | All FR |                  
|  NFR2  | Usability | The prices should be in euro | All FR |      
|  NFR3  | Performance | All functions should be completed in less than 0.5 seconds  | All FR |                
|  NFR4  | Reliability | The application should show the most updated and real information | All FR |     
|  NFR5  | Localisation | Decimal numbers use . (dot) as decimal separator ||


# Use case diagram and use cases

## Use case diagram

```plantuml
left to right direction
actor User as u
actor RegisteredUser as ru
actor Administrator as a

rectangle system{
  u -- (Search information)
  ru -- (Search information)
  ru -- (Login)
  ru -- (Update prices)   
  ru -- (Gas Station management) : propose 
  u  -- (Registration)
  a -- (RegisteredUsers management)
  a -- (Requests management) 
  (Update prices) .> (Login) : <<include>> 
  (Gas Station management) ..> (Login) : <<include>> 
  (Gas Station management) <... (Add) : <<extend>>
  (Gas Station management) <... (Update) : <<extend>>
  (Gas Station management) <... (Delete) : <<extend>>
}
```

## Use Cases

### Use case 1, UC1 - FR4.1 Add a Gas station

| Actors Involved        | RegisteredUser |   
| ------------- |:-------------:|    
|  Precondition     | RegisteredUser RU made the Login |     
|  Post condition     | No duplication of Gas stations|
|  Nominal Scenario     | RU enter the address| 
| |  RU enter the name and address of the gas station| 
| |  RU enter the fuel names and prices. |
| |  Administrator accepts the request|
| | A Gas station has been added   |

### Use case 2, UC2 - FR4.2 Modify a Gas station

| Actors Involved        | RegisteredUser |   
| ------------- |:-------------:|    
|  Precondition     | RegisteredUser RU made the Login |     
|  Post condition     | No duplication of station |   
|  Nominal Scenario     | RU choose a Gas station to modify | 
| |  RU the fields to modify | 
| |  RU the new value values |
| |  Administrator accepts the request| 
| | A Gas station has been modified |

### Use case 3, UC3 - FR4.3 Delete a Gas station

| Actors Involved        | RegisteredUser |   
| ------------- |:-------------:|    
|  Precondition     | RegisteredUser RU made the Login |     
|  Post condition     | Good reason for deleting (Gas station has been closed, duplication...) & reliability score is good enough |
|  Nominal Scenario     | RU choose a Gas station to modify |  
| |  RU chooses to delete it | 
| |  RU enters the reason of the deletion |
| |  Administrator accepts the request| 
| | The Gas station has been deleted |

### Use case 4, UC4 - FR5 Update a fuel price

| Actors Involved        | RegisteredUser |   
| ------------- |:-------------:|     
|  Precondition     | RegisteredUser RU made the Login & his reliability score is good enough |     
|  Post condition     | New price not to far from previous one |    
|  Nominal Scenario     | RU selects a Gas station|  
| | RU selects a fuel type |  
| | RU enters the new fuel price |   
|  Variants     | The fuel type does not exist: this needs an update of fuel types list |    

### Use case 5, UC5 - FR7 Registration

| Actors Involved        | User |   
| ------------- |:-------------:|     
|  Precondition     | User U owns an email |      
|  Post condition     | New RegisteredUser created |  
| | No duplication of email or phone number (security) |   
|  Nominal Scenario     | U chooses to register |  
| | U enters name, surname, email and phone number |  
| | U validates his email |   
| | New RegisteredUser created |  
|  Variants     | Duplication of email or phone number: issue warning |   

### Use case 6, UC6 - FR3 Search information

| Actors Involved        | User |   
| ------------- |:-------------:|     
|  Precondition     | User U has an accessible position |      
|  Post condition     | |   
|  Nominal Scenario     | U opens the application  |  
| | The default researchs are made by distance |  
|  Variants     | U selects a specific fuel type FT | 
| | U decide to order Gas stations by price (filtered by FT) |

### Use case 7, UC7 - FR6 Login

| Actors Involved        | RegisteredUser  |
| ------------- |:-------------:| 
|  Precondition     | The RegisteredUser RU is registered by definition |  
|  Post condition     | RU enters into its personal area |
|  Nominal Scenario     | RU inserts username and password |
|| The system confirms and validates|
|  Variants     | Invalid username or/and password: issue error. |
| | RU forgets his password |


### Use case 8, UC8 - FR8 Users Management

| Actors Involved        | Administrator  |
| ------------- |:-------------:| 
|  Precondition     | The Administrator A is located on the application local server to access to his personal area |  
|  Post condition     | The RegisteredUser is now ignored by the system |
|  Nominal Scenario     | A bans a RegisteredUser (makes him ignored by the system) because of his actions and reliability score|

### Use case 9, UC10 - FR9 Requests management

| Actors Involved        | Administrator  |
| ------------- |:-------------:| 
|  Precondition     | The Administrator A is located on the application local server to access to his personal area | 
| | A receives a RegisteredUser request (addition, modification or deletion of a Gas station)| 
|  Post condition     | The request is managed (accepted/delcined)|
|  Nominal Scenario    | A reads the details of the request |
|| A verifies the validity of the information |
| | A choose to accept or decline the request (if the request is declined, the reliability score of the user will be decreased) |



# Relevant scenarios

## Scenario 1

| Scenario ID: SC1        | Corresponds to UC1  |   
| ------------- |:-------------|    
| Description | RefisteredUser RU add a Gas station |    
| Precondition | RegistreredUser has logged in |   
| Postcondition | Request is sent to the Administrator |   
| Step#        |  Step description   |    
|  1     | RU select to add a new Gas station |      
|  2     | RU enters the Gas station name |       
|  3     | RU enters tha Gas station address (it can be : my current location) |     
|  4     | RU enter fuel types and their prices | 
|  5     | System asks to RU to confirm |
|  6     | Request is sent to the Administrator |   

## Scenario 2

| Scenario ID: SC2        | Corresponds to UC2  |   
| ------------- |:-------------|    
| Description | RegisteredUser RU modifies a Gas station |    
| Precondition | RegistreredUser has logged in |   
| Postcondition | Request is sent to the Administrator |   
| Step#        |  Step description   |    
|  1     | RU selects a Gas station GS |      
|  2     | RU selects to modify GS|       
|  3     | RU selects GS fields to modify (address, name...)|     
|  4     | RU enter the new values | 
|  5     | System asks to RU to confirm |
|  6     | Request is sent to the Administrator |  

## Scenario 3

| Scenario ID: SC3        | Corresponds to UC2  |   
| ------------- |:-------------|    
| Description | RegisteredUser RU deletes a Gas station |    
| Precondition | RegistreredUser has logged in |   
| Postcondition | Request is sent to the Administrator |   
| Step#        |  Step description   |    
|  1     | RU select a Gas station GS|          
|  2     | RU select to delete GS|     
|  3     | RU enter the reasons | 
|  4     | System asks to RU to confirm |
|  5     | Request is sent to the Administrator |

## Scenario 4

| Scenario ID: SC4        | Corresponds to UC4 |    
| ------------- |:-------------|      
| Description | RegisteredUser RU update a Gas station fuel price |   
| Precondition | RegistreredUser has logged in & his reliability score is high  enough|   
| Postcondition | The request is processed |   
| Step#        |  Step description   |    
|  1     | RU selects a Gas station GS|      
|  2     | RU selects GS fuel type to update |   
|  3     | RU enters the new price |   
|  4     | System ask to RU to confirm |
|  5     | The request is processed |   

## Scenario 5

| Scenario ID: SC5        | Corresponds to UC5 |    
| ------------- |:-------------|    
| Description | User Registration |    
| Precondition | User U owns an email |     
| Postcondition | New RegisteredUser created |  
| | No duplication of email or phone number |    
| Step#        |  Step description   |    
|  1     | U enters his personal information (email, phone number...) |      
|  2     | System checks the validity of email and phone number |   
|  3     | System sends a verification email |    
|  4     | U verifies his email |  
|  5     | New RegisteredUser is created |  

## Scenario 6

| Scenario ID: SC6        | Corresponds to UC6 |    
| ------------- |:-------------| 
| Description | Search a Gas station |
| Precondition | User U has an accessible position |
| Postcondition |  |
| Step#        | Step description  |
|  1     | The application is opened on the Search Page |  
|  2     | U selects how to filter information |
|  3     | The filtered Gas stations list is shown  |

## Scenario 7

| Scenario ID: SC7        | Corresponds to UC7 |    
| ------------- |:-------------| 
| Description | Login operation to allow RegisteredUsers to modify Gas stations |
| Precondition | The RegisteredUser RU is registered by definition  | 
| Postcondition |  RU enters into its personal area |
| Step#        | Step description  |
|  1     | User U selects Login |  
|  2     | U enters its credentials |
|  3     | U's credentials are correct  |
|  4     | U is now logged in and he will be consider a RegisteredUser |

## Scenario 8

| Scenario ID: SC8        | Corresponds to UC8 |    
| ------------- |:-------------| 
| Description | The Administrator A bans a RegisteredUser RU bacause of his actions or his low reliability |
| Precondition | The Administrator A is located on the application local server to access to his personal area |
| Postcondition | RU is now ignored by the system |
| Step#        | Step description  |
|  1     | A can see RegisteredUsers with a low reliability and their actions |  
|  2     | A bans a RegisteredUser |

## Scenario 9

| Scenario ID: SC9        | Corresponds to UC9 |    
| ------------- |:-------------| 
| Description | Requests Management |
| Precondition | The Administrator A is located on the application local server to access to his personal area & A received a Request |
| Postcondition | The request is treated  |
| Step#        | Step description  |
|  1     | A verifies the validity of the request's information |
|  2     | A choose to accept or decline the request  |
| 3 | If the request is declined, the reliability score of the user will be decreased|


# Glossary

```plantuml
class EZgas

class User {
+ Uid
}

class RegisteredUser {
+ reliability
+ UName
+ surname
+ mailAddress
+ phoneNumber
}
note right of RegisteredUser: Logged user with privileges:\n he can update prices and \nmodify Gas stations

class Administrator {

}

class GasStation {
+ GSid
+ GSName
}

class Position {
+ coordinates
+ address
}

class Fuel {
+ price
}

class FuelType {
+ Name
}

class Research {
+ orderType
+ maxDistance
+ maxNumber
}
note left of Research: Research made by an user \nto find Gas stations

class Request {
+ Rid
+ type
+ content
}
note right of Request: Request sended by a RegisteredUser\n to the Administrator to add,\n delete or update Gas stations

EZgas -- "*" User
EZgas -- "*" GasStation
RegisteredUser .. EZgas : registered in

User -- "*" Research : makes

User -- "0.1" Position
GasStation *-- Position
Research *-- Position

RegisteredUser --|> User

GasStation -- "*" Fuel

Fuel *-- FuelType
Research *-- FuelType

RegisteredUser .. Fuel : update
RegisteredUser -- "*" Request : send
Request --* GasStation
Administrator --"*" Request : manage
Administrator .. RegisteredUser : manage
Administrator .. EZgas : part of
```

