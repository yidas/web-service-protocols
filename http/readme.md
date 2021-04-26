TCP
===

#### Sequence Diagram

```plantuml
@startuml
participant "Client" as c
participant "Server" as s

c->s: GET HTTP/1.1
s->c: HTTP/1.1 200 OK
...
c->s: POST HTTP/1.1
s->c: HTTP/1.1 201 Created

@enduml

```

#### Sequence Diagram

```plantuml

```

References
----------

[Wikipedia - Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
