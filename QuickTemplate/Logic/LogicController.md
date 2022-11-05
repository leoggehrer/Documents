# Logic-Kontroller

Im Projekt ***Logic*** gibt es zu jeder Entitaet einen Kontroller mit der Namenskonvention *Entitaet im plural* und dem Postfix *Controller* und befinden sich im Ordner ***Controllers***. Abgeleitet werden diese Kontroller vom generischen Kontroller **GenericController\<T>**. Mit der Ableitung, vom generischen Kontroller, erben die Kontroller die Standard Operationen (CRUD...Create Read Update and Delete).  

Die Aufgabe eines Kontrollers ist die Kontrolle des Zugriffes und die Pruefung der Dateninhalte der entsprechende Entitaet. Bevor die Entitaet in der Persistierungsschicht (Datenbank) gespeichert wird, werden .
 kontrolliert den Zugriff auf eine Entitaet und uebernimmt die
Ein Kontroller

 (es gibt fuer jede Entitaet einen Kontroller) befindet sich die Geschaeftslogik vom Backend. Zu jeder Entitaet gibt es einen konkreten Kontroller welcher sich vom generischen Kontroller ableitet. Zum Beispiel ist der Kontroller fuer die Entitaet **Customer**  befindet sich die Geschaeftslogik.

## Kontroller

Im Kontroller

## Insert-Opertaion

### Sequence diagram (SD) "TEntity InsertAsync(TEntity entity)"

![your-UML-diagram-name](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/plantuml-markdown/main/example.plantuml
)

![Test](https://raw.githubusercontent.com/leoggehrer/CSHtlLeoTemplate-QuickTemplate/dd093bcb545ad6c5d2d3bdc28c06dde705e5bb0f/AspMvcDefaultSharedViews-Index.png)

```plantuml
@startuml Controller Insert Part 1
skinparam {
    monochrome false
    sequenceArrowThickness 2
    maxmessagesize 60
}

title Ablauf Insert-Operation

'deklaration
actor client
participant "InsertAsync\n(entity)" as insert
participant "Check-\nAuthorizationAsync\n(type, actionName)" as checkauth
participant "Execute-\nInsertAsync\n(entity)" as execute
participant "BeforeReturn\n(entity)" as beforeret
participant "ValidateEntity\n(actionType, entity)" as validate
participant "Before-\nActionExecute\n(actionType, entity)" as beforeaction
participant "Before-\nExecuteInsert\n(entity)" as beforeinsert
participant "EntitySet\n.AddAsync\n(entity)" as add
participant "After-\nExecuteInsert\n(entity)" as afterinsert
participant "After-\nActionExecute\n(actionType, entity)" as afteraction
'declaration

client -> insert : entity
activate insert
alt if (ACCOUNT_ON)
insert -> checkauth : type, "InsertAsync"
activate checkauth
note right: Optional: Aufruf nur wenn ACCOUNT_ON ist
return
end
insert -> execute : entity
activate execute

'Beginn: Ablauf ExecuteInsert(...)
execute -> validate : Insert, entity
activate validate
return

execute -> beforeaction : Insert, entity
activate beforeaction
return

execute -> beforeinsert : entity
activate beforeinsert
return

execute -> add : entity
activate add
return

execute -> afterinsert : entity
activate afterinsert
return

execute -> afteraction : Insert, entity
activate afteraction
return

'Ende: Ablauf ExecuteInsert(...)
execute --> insert : result
deactivate execute

insert -> beforeret : result
activate beforeret
return result
insert --> client : result
deactivate insert
@enduml
```

### Activity diagram (AD) "TEntity InsertAsync(TEntity entity)"

```plantuml
@startuml
skinparam {
    monoChrome false
    rectangleRoundCorner 15
    rectangleBackgroundColor #smokewithe
}

rectangle "TEntity InsertAsync(TEntity entity)" { 
    start
    if (ACCOUNT_ON?) then (yes)
    :CheckAuthorizationAsync(Insert, entity);
    else (no)
    endif
    :result = ExecuteInsertAsync(entity);
    :return BeforeReturn(result);
    stop
}
@enduml
```

> HINWEIS:
> Ist die Direktive ***ACCOUNT_ON*** definiert, dann wird die Benutzerberechtigung geprueft.

#### Activity diagram (AD) "TEntity ExecuteInsertAsync(TEntity entity)"

```plantuml
@startuml
skinparam {
    monoChrome false
    rectangleRoundCorner 15
    rectangleBackgroundColor #smokewithe
}

rectangle "TEntity ExecuteInsertAsync(TEntity entity)" { 
    start
    :ValidateEntity(entity);
    :BeforeActionExecute(Insert, entity);
    :BeforeExecuteInsert(entity);
    :EntitySet.AddAsync(entity);
    :AfterExecuteInsert(entity);
    :AfterActionExecute(Insert, entity);
    stop
}
@enduml
```

> Hinweis:  
> Alle angefuerten Methoden sind mit ***virtual*** spezifiziert und koennen in der Unterklasse angepasst (ueberschrieben ***override***) werden.

