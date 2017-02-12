---
layout: home
title: Booster2
---


<div style="text-align:center;margin:0 10px 10px 0" markdown="1">
![](figs/booster-rocket.png){:width="200px"}
</div>

## What is Booster2?

B Object Oriented STate-based Refinement or Booster is a notation and supporting tool for converting system specifications into online information systems. This implementation, Booster2, uses revised underlying architecture. The revised tool generates standard SQL schemas and stored procedures, and is defined using the Spoofax language workbench. This is in contrast with the original implementation which created Abstract Machines for the B-Toolkit and resulted in C code with an in-memory database.

Booster2 is designed for information systems where the specification is expected to evolve in response to changing requirements. In typical development, requirements changes after software delivery involve costly and lengthy redesign processes. Changes to specification are reflected in new generated implementation. Booster uses a generic entity notation for classes and attributes. Specifications are created with invariants, and method specified as pre- and post- conditions. The tool generates database schemas, stored procedures, an API and a user interface from a high-level system specification.

## Booster Notation

Booster files use the `boo2` file extension. Lets start with this example application for a Library system.

```
 system Library

  class Book {
    attributes
      title : String
      borrower : [Reader.borrowed]
      owner : Lender.holdings
    invariants
      owner : borrower.subs
  }

  class Reader {
    attributes
      name : String
      borrowed : set(Book.borrower)[*]
      subs : set(Lender.members)[*]
    methods
      subscribe { 
        lender? : subs' 
      }
      borrow{ 
        book?.borrower = null 
        book? : borrowed' 
      }
      returnBook{ 
        b? : borrowed 
        b? /: borrowed' 
      }
  }

  class Lender {
    attributes
      max : Int
      members : set(Reader.subs)[*]
      holdings : set(Book.owner)[*]
    invariants
      card(members) <= max
  }

}
```

Lets walk though this specification.

#### Systems
```system Library``` 

This sets the name of the system and will be used to create the database tables.


#### Classes
```
  class Book {

  }
```

These are the classes of the system, which are made up of attributes, methods and invariants.

#### Primitive Attributes

The simplest kinds of attribute, where attribute name is followed by either `Boolean`, `Int` or `String`.

```
class Book {
    attributes
      title : String
}

class Lender {
    attributes
      max : Int
}
```


#### Reference Valued Attributes

Classes can hold two-way references to other classes.

```
class Book {
    attributes
        borrower : [Reader.borrowed]
}

class Reader {
    attributes
        borrowed : set(Book.borrower)[*]
}
```

A `Book` has a `borrower`, of type `Reader`, the opposite attribute is `Reader.borrowed`. 

A `Reader` has a `set` of `borrowed` `Book`s, where the opposite is attribute is `Book.borrower`.

This enforces navigability of references.


#### Invariants

```
  class Lender {
    attributes
      max : Int
      members : set(Reader.subs)[*]
    invariants
      card(members) <= max
  }
```

The `Lender` class has an invariant which restricts the number of members to less-than or equal-to ```max```. The number of members is the `card()` (cardinality) of the `members` set.

#### Methods

```
  class Reader {
    attributes
      borrowed : set(Book.borrower)[*]
    methods
      returnBook{ 
        b? : borrowed 
        b? /: borrowed' 
      }
   }
```

The `returnBook` method takes `b?`, an element of the `borrowed` set as argument. The `b?` argument must not be an element of the `borrowed'` set after the method completes. 

The `:` operator can be read as "element of", `/:` can be read as "not an element of". The `?` identifies the `b` as an argument of the method. The post-state of the `borrowed` set is indicated by the prime symbol `'`.



## Screenshots

[![The Booster Tool](figs/booster-tool.png){:width="300px"}](figs/booster-tool.png)

[![A Generated Script (In mysql workbench)](figs/booster-generated-db-script.png){:width="300px"}](figs/booster-generated-db-script.png)

[![The login for a generated system](figs/booster-system-login-window.png){:width="300px"}](figs/booster-system-login-window.png)

[![The main Booster interface](figs/booster-system-main-interface.png){:width="300px"}](figs/booster-system-main-interface.png)

[![The Booster Object viewer](figs/booster-object-view.png){:width="300px"}](figs/booster-object-view.png)

[![A Booster generated edit method](figs/booster-generated-method.png){:width="300px"}](figs/booster-generated-method.png)

## Install Instructions

### Docker Image

- Install Docker
- Clone the Booster Docker repository
- Copy a Booster2 specification into files/
- build the Docker image 

``docker build . -t `whoami`/booster2:proto``

- run the docker image 

``docker run -p 80:8080  -v `pwd`/files:/files `whoami`/booster2:proto myboosterspec.boo2``

- (optional) copy a database populate script into files/
- navigate to [http://localhost:80/gwi](http://localhost:80/gwi) login to browse your data
- login and password are set to the system name

To get an Eclipse based Booster2 editor and translator, follow the developer steps below.

### Developers

- Install the Spoofax 2.0.0-beta Eclipse distribution
- Clone the Booster 2.0 repository
- Import the Booster2 folder (as a Maven project) into your Spoofax Eclipse
- install maven 3.3.9 and configure Eclipse to use it, the embedded Maven has a sl4j bug.
- (optional) Install Jave EE into your Eclipse 
- (optional) Install Tomcat and integrate with Eclipse 
- (optional) Install MySQL 5.6

## People

People who have contributed to Booster2.

- James Welch
- Daco Harkes
- Ed Crichton
- [Seyyed Shah](http://sshah.co.uk)

## Technology

- Metaborg Spoofax Language Workbench
- MySQL
- Apache Tomcat

## Funding

The development of Semantic Booster been supported by the [ALIGNED](http://aligned-project.eu/)
Project, a European Union Horizon 2020 Framework project. Number: #644055.


