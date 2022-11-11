# Logic-Controller

Im Projekt ***Logic*** gibt es zu jeder Entitaet einen Kontroller mit der Namenskonvention *Entitaet im Plural* und dem Postfix *Controller*. Diese Kontroller befinden sich in den Unterordnern von ***Controllers***. Die Unterordner ergeben sich aus der Ordnerstruktur der Entities. Befindet sich die Entitaet ***Customer*** im Ordner ***Entities/Base***, dann befindet sich der entsprechende Kontroller im Ordner ***Controllers/Base***.

Aufgabe eines Kontrollers ist die Steuerung des Zugriffes und die Pruefung der Dateninhalte der entsprechende Entitaet. Bevor die Entitaet in der Persistierungsschicht (Datenbank) gespeichert wird, werden .
 kontrolliert den Zugriff auf eine Entitaet und uebernimmt die

Abgeleitet werden diese Kontroller vom generischen Kontroller **GenericController\<T>**. Mit der Ableitung, vom generischen Kontroller, erben die Kontroller die Standard Operationen (CRUD...Create Read Update and Delete).  

Ein Kontroller

 (es gibt fuer jede Entitaet einen Kontroller) befindet sich die Geschaeftslogik vom Backend. Zu jeder Entitaet gibt es einen konkreten Kontroller welcher sich vom generischen Kontroller ableitet. Zum Beispiel ist der Kontroller fuer die Entitaet **Customer**  befindet sich die Geschaeftslogik.

## Kontroller

Im Kontroller

## Insert-Operation

### Sequence diagram (SD) "TEntity InsertAsync(TEntity entity)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/SD_InsertAsync.plantuml)

### Activity diagram (AD) "TEntity InsertAsync(TEntity entity)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_InsertAsync.plantuml)

> HINWEIS:
> Ist die Direktive ***ACCOUNT_ON*** definiert, dann wird die Benutzerberechtigung geprueft.

#### Activity diagram (AD) "TEntity ExecuteInsertAsync(TEntity entity)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_ExecuteInsertAsync.plantuml)

> Hinweis:  
> Alle angefuerten Methoden sind mit ***virtual*** spezifiziert und koennen in der Unterklasse angepasst (ueberschrieben ***override***) werden.

## Update-Operation

### Sequence diagram (SD) "TEntity UpdateAsync(TEntity entity)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/SD_UpdateAsync.plantuml)

### Activity diagram (AD) "TEntity UpdateAsync(TEntity entity)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_UpdateAsync.plantuml)

> HINWEIS:
> Ist die Direktive ***ACCOUNT_ON*** definiert, dann wird die Benutzerberechtigung geprueft.

#### Activity diagram (AD) "TEntity ExecuteUpdateAsync(TEntity entity)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_ExecuteUpdateAsync.plantuml)

> Hinweis:  
> Alle angefuerten Methoden sind mit ***virtual*** spezifiziert und koennen in der Unterklasse angepasst (ueberschrieben ***override***) werden.

## Delete-Operation

### Sequence diagram (SD) "void DeleteAsync(int id)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/SD_DeleteAsync.plantuml)

### Activity diagram (AD) "void DeleteAsync(int id)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_DeleteAsync.plantuml)

> HINWEIS:
> Ist die Direktive ***ACCOUNT_ON*** definiert, dann wird die Benutzerberechtigung geprueft.

#### Activity diagram (AD) "void ExecuteDeleteAsync(int id)"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_ExecuteDeleteAsync.plantuml)

> Hinweis:  
> Alle angefuerten Methoden sind mit ***virtual*** spezifiziert und koennen in der Unterklasse angepasst (ueberschrieben ***override***) werden.

## SaveChanges-Operation

### Sequence diagram (SD) "int SaveChangesAsync()"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/SD_SaveChangesAsync.plantuml)

### Activity diagram (AD) "int SaveChangesAsync()"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_SaveChangesAsync.plantuml)

> HINWEIS:
> Ist die Direktive ***ACCOUNT_ON*** definiert, dann wird die Benutzerberechtigung geprueft.

#### Activity diagram (AD) "int ExecuteSaveChangesAsync()"

![SD-InsertAsync](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/leoggehrer/Documents/master/QuickTemplate/Logic/AD_ExecuteSaveChangesAsync.plantuml)

> Hinweis:  
> Alle angefuerten Methoden sind mit ***virtual*** spezifiziert und koennen in der Unterklasse angepasst (ueberschrieben ***override***) werden.
