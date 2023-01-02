# QuickTemplate  
  
Das Projekt ***QuickTemplate*** ist eine Vorlage fuer die Erstellung von datenzentrierten Anwendungen. Ausgehend von dieser Vorlage koennen neue Anwendungen, sogenannte Domain-Projekte, erstellt, erweitert und angepasst werden.  
  
## Inhaltsverzeichnis

- [QuickTemplate](#quicktemplate)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
  - [Infrastruktur](#infrastruktur)
  - [Template](#template)
  - [Entwicklerwerkzeuge](#entwicklerwerkzeuge)
  - [Verwendung der Vorlage](#verwendung-der-vorlage)
  - [System-Erstellungs-Prozess](#system-erstellungs-prozess)
    - [Vorbereitungen](#vorbereitungen)
    - [Projekterstellung](#projekterstellung)
  - [Abgleich mit dem QuickTemplate](#abgleich-mit-dem-quicktemplate)
  - [Setzen von Preprozessor-Defines](#setzen-von-preprozessor-defines)
- [Umsetzungsschritte](#umsetzungsschritte)
  
## Infrastruktur  
  
Zur Umsetzung des Projektes wird DotNetCore (7.0 und hoeher) als Framework, die Programmiersprache CSharp (C#) und die Entwicklungsumgebung Visual Studio 2022 Community verwendet. Alle Komponenten koennen kostenlos aus dem Internet heruntergeladen werden.  
  
In diese Dokumentation werden unterschiedliche Begriffe verwendet. In der nachfolgenden Tabelle werden die wichtigsten Begriffe zusammengefasst und erlaeutert:  

|Begriff|Bedeutung|Synonym(e)|
|---|---|---|
|**Solution**|Ist eine Zusammenstellung von verschiedenen Teilprojekten zu einer Gesamtloesung.|Gesamtloesung, Loesung, Projekt|
|**Domain Solution**|Damit ist eine Gesamtloesung gemeint, welches fuer einen bestimmten Problembereich eine Loesung darstellt.|Problemloesung, Projekt|
|**Teilprojekt**|Ist die Zusammenfassung von Klassen und/oder Algorithmen, welches eine logische Einheit fuer die Loesungen bestimmter Teilprobleme bildet.|Teilloesung, Projekteinheit, Projekt|
|**Projekttyp**|Unter Projekttyp wird die physikalische Beschaffenheit eines Projektes bezeichnet. Es gibt zwei grundlegende Typen von Projekten: <br>  - Ein wiederverwendbares Projekt (z.B.: eine Bibliothek) und <br>  - ein ausfuehrbares Projekt (z.B.: eine Konsolenanwendung, WepApi, AspMvc usw.). <br>**Als Regel gilt:**<br> Alle Programme und Algorithmen werden in den *wiederverwendbaren Projekten* implementiert. Die ausfuehrbaren Einheiten dienen nur als Startprojekte und leiten die Anfragen an die *wiederverwendbaren Komponenten* weiter.|Bibliothekstyp, Consolentyp|
|**Library oder Bibliothek**|Kennzeichnet einen *wiederverwendbaren Projekttyp*.|Bibliothek|
|**Console**|Kennzeichnet einen *ausfuehrbaren Projekttyp*. Dieser Typ startet eine Konsole fuer die Programmausfuehrung.|Konsole|
|**Host**|Dieser Typ kennzeichnet ein *ausfuehrbares Projekt*, welches zum Starten den IIS verwendet oder im Modus `selfhosting` gestartet werden kann.|Web-Application |
|**Abhaengigkeit**|Die Abhaengikeit beschreibt die Beziehungen von Projekten untereinander. Benoetigt ein *Projekt A* Funktionalitaeten aus einem *Projekt B*, so wird eine Projektreferenz vom *Projekt B* in *Projekt A* benoetigt.|Projektreferenz, Referenz, Dependency, Projektverweis|
  
## Template  

Die Struktur vom **QuickTemplate** besteht aus unterschiedlichen Teilprojekten und diese sind in einer Gesamtloesung (im Kontext von Visual Studio ist das eine Solution) zusammengefasst. Eine Erlaeuterung der einzelnen Projekte, deren Typ und die Abhaengigkeit finden sie in der folgenden Tabelle:  
  
|Projekt|Beschreibung|Typ|Abhaengigkeit|
|---|---|---|---|
|**CommonBase**|In diesem Projekt werden alle Hilfsfunktionen und allgemeine Erweiterungen zusammengefasst. Diese sind unabhaengig vom Problembereich und koennen auch in andere Domaen-Projekte wiederverwendet werden.|Library|keine|
|**QuickTemplate.Logic** <br>oder<br> **QuickTemplate.AppLogic** (MacOS)|Dieses Projekt beinhaltet den vollstaendigen Datenzugriff, die gesamte Geschaeftslogik und stellt somit den zentralen Baustein des Systems dar.|Library|CommonBase|
|**QuickTemplate.Logic.UnitTest**|In diesem Projekt befinden sich die Unit-Tests fuer die gesamte Geschaeftslogik.|MSTest|CommonBase, QuickTemplate.Logic (.AppLogic)|
|**QuickTemplate.WebApi**|In diesem Projekt ist die REST-Schnittstelle implementiert. Dieses Modul stellt eine API (Aplication Programming Interface) fuer den Zugriff auf das System ueber das Netzwerk zur Verfuegung.|Host|CommonBase, QuickTemplate.Logic (.AppLogic)|
|**QuickTemplate.ConApp**|Dieses Projekt dient als Initial-Anwendung zum Erstellen der Datenbank, das Anlegen von Anmeldedaten falls die Authentifizierung aktiv ist und zum Importieren von bestehenden Daten. Nach der Initialisierung wird diese Anwendung kaum verwendet.|Console|CommonBase, QuickTemplate.Logic (.AppLogic)|
|**QuickTemplate.AspMvc**|Diese Projekt beinhaltet die Basisfunktionen fuer eine AspWeb-Anwendung und kann als Vorlage fuer die Entwicklung einer AspWeb-Anwendung mit dem QuickTemplate verwendet werden.|Host|CommonBase, QuickTemplate.Logic (.AppLogic)|
|**QuickTemplate.WpfApp**|Diese Projekt beinhaltet die Basisfunktionen fuer eine Wpf-Anwendung und kann als Vorlage fuer die Entwicklung einer einer Wpf-Anwendung mit dem QuickTemplate Framework verwendet werden.|Host|CommonBase, QuickTemplate.Logic (.AppLogic)|
|**QuickTemplate.XxxYyy**|Es folgen noch weitere Vorlagen von Client-Anwendungen wie Angular, Blazor und mobile Apps. Zum jetzigen Zeitpunkt existiert nur die AspMvc-Anwendung und Wpf-Anwendung. Die Erstellung und Beschreibung weiterer Client-Anwendungen erfolgt zu einem spaeteren Zeitpunkt.|Host|CommonBase, QuickTemplate.Logic (.AppLogic)|
  
## Entwicklerwerkzeuge  

Dem Entwickler stehen unterschiedliche Hilfsmittel fuer die Erstellung von Projekten zur Seite. Die wichtigsten Werkzeuge sind in der nachfolgenden Tabelle zusammengefasst:  
  
|Projekt|Beschreibung|Typ|Abhaengigkeit  
|---|---|---|---|
|**TemplateCodeGenerator.Logic** <br>oder<br> **TemplateCodeGenerator.AppLogic** (MacOS)|In diesem Modul befinden sich die Komponenten zur Code-Generierung. Eine genauere Beschreibung der Komponenten erfolgt zu einenem spaeteren Zeitpunk.|Library|CommonBase  
|**QuickTemplate.CodeGenApp**|Diese Anwendung startet die Code-Generierung fuer das Projekt in dem es enthalten ist. <br>**Voraussetzung:**<br> Die Code-Generierung verwendet die Meta-Information der Logik (XY.Logic oder XY.AppLogic). Das bedeuted allerdings, dass die Bibliothek fehlerfrei ueberstezt werden kann. Nur so kann die Meta-Information aus Logik gelesen und fuer die Code-Generierung verwendet werden.|Console|CommonBase, TemplateCodeGenerator.Logic (.AppLogic)
|**TemplateTools.ConApp**|Diese Anwendung ist eine Zusammenfassung von unterschiedlichen Werkzeugen welche mit dem ***'QuickTemplate'*** verwendet werden koennen. Folgende Werkzeuge befinden sich in der Sammlung:<br>- **Copier**...kopiert alle Teilprojekte aus der Vorlage ***'QuickTemplate'*** in das angegebenen Zielverzeichnis und fuehrt eine Umbenennung der Komponenten durch.<br>- **Preprocessor**...dient zum Setzen der Definitionen (z.B. ACCOUNT_ON usw.) in der entspechenden Solution. <br>- **Code-Generierung**...Mit dieser Auswahl kann die Code-Generierung aktiviert werden.<br>-**Comparison**...Diese Funktion dient zum Abgleich der Vorlage ***'QuickTemplate'*** mit den bereits erstellten ***'Domain-Projekten'***.|Console|CommonBase  
  
## Verwendung der Vorlage
  
Nachfolgend werden die einzelnen Schritte von der Vorlage ***QuickTemplate*** bis zum konkreten Projekt ***QTMusicStoreLight*** erlaeutert. Das Projekt ist eine einfache Anwendung zur Demonstration von der Verwendung der Vorlage. Im Projekt ***QTMusicStoreLight*** werden Kuenstler (Artisten) und deren produzierten Alben verwaltet. Jedes Album hat ein Genre (Rock, Pop, Klassik usw.) zugeordnet. Ein Datenmodell ist im nachfolgendem Abschnitt definiert.  

## System-Erstellungs-Prozess  
  
Wenn nun ein einfacher Service oder eine Anwendung entwickelt werden soll, dann kann die Vorlage ***QuickTemplate*** als Ausgangsbasis verwendet und weiterentwickelt werden. Dazu empfiehlt sich folgende Vorgangsweise:  
  
### Vorbereitungen  
  
- Erstellen eines Ordners (z.B.: Develop)  
- Herunterladen des Repositories ***QuickTemplate*** vom [GitHub](<https://github.com/leoggehrer/CSTemplate-QuickTemplate>) und in einem Ordner speichern.  
  
> **ACHTUNG:** Der Solution-Ordner von der Vorlage muss ***QuickTemplate*** heißen.  
  
### Projekterstellung  

Die nachfolgenden Abbildung zeigt den schematischen Erstellungs-Prozess fuer ein Domain-Projekt:  
  
![Create domain project overview](CreateProjectOverview.png)  
  
Als Ausgangsbasis wird die Vorlage ***QuickTemplate*** verwendet. Diese Vorlage wird mit Hilfe dem Hilfsprogramm ***'TemplateTools.ConApp'*** in ein Verzeichnis eigener Wahl kopiert. Bei der Erstellung des Domain-Projektes **QTMusicStoreLight** werden die folgenden Aktionen ausgefuehrt:

- Alle Projektteile aus der Vorlage werden in das Zielverzeichnis kopiert.
- Die Namen der Projekte und Komponenten werden entsprechend angepasst.
- Alle Projekte mit dem Prefix **QuickTemplate** werden mit dem domainspezifischen Namen erstezt.
- Beim Kopieren der Dateien wird der Label **@BaseCode** mit dem Label **@CodeCopy** ersetzt (Diese Labels werden fur einen späteren Abgleich-Prozess verwendet).

Nachfolgend wird die Erstellung des Beispiel-Projektes **QTMusicStoreLight**  mit dem Werkzeug **TemplateTools.ConApp** demonstriert:
  
```csharp
Template Tools
==============

Choose a tool:

[1] Copier..........Copy a quick template to a project
[2] Preprocessor....Setting defines for project options
[3] CodeGenerator...Generate code for template solutions
[4] Comparison......compares a project with the template and compares it
[x|X] Exit

Choose: 1
```

Nach der Bestaetigung der Auswahl erscheint die folgende Bildschirmmaske:

```csharp
Template Copier
===============

Copy 'QuickTemplate' from: /Users/ggehrer/Projects/CSMacTemplate/QuickTemplate
Copy to 'TargetSolution':   /Users/ggehrer/Projects/CSMacTemplate/TargetSolution

[1] Change source path
[2] Change target path
[3] Change target solution name
[4] Start copy process
[x|X] Exit

Choose: 
```

Nun muessen die Parameter **Target path** und **Target solution name** eingestellt werden.

```csharp
Template Copier
===============

Copy 'QuickTemplate' from: /Users/ggehrer/Projects/CSMacTemplate/QuickTemplate
Copy to 'QTMusicStoreLight':   /Users/ggehrer/Projects/Sample/QTMusicStoreLight

[1] Change source path
[2] Change target path
[3] Change target solution name
[4] Start copy process
[x|X] Exit

Choose: 4
```

**Hinweis:** Die Vorlage muss in einem Ordner mit dem Namen **QuickTemplate** gespeichert sein.  
  
Nach der Ausfuehren der Option ***'[4] Start copy process'*** befindet sich folgende Projektstruktur im Ordner **...\QTMusicStoreLight**:  
  
- CommonBase  
- QTMusicStoreLight.AppLogic
- QTMusicStoreLight.AspMvc
- QTMusicStoreLight.CodeGenApp
- QTMusicStoreLight.ConApp
- QTMusicStoreLight.Logic.UnitTest
- QTMusicStoreLight.WebApi
- QTMusicStoreLight.WpfApp
- TemplateCodeGeneration.AppLogic
- TemplateTools.ConApp
  
In der Vorlage ***QuickTemplate*** sind alle Code-Teile, welche als Basis-Code in andere Projekte verwendet werden, mit einem Label ***@BaseCode*** markiert. Dieser Label wird im Zielprojekt mit dem Label ***@CodeCopy*** ersetzt. Das hat den Vorteil, dass Aenderungen in der Vorlage auf die bereits bestehenden Projekte uebertragen werden koennen (naehere Informationen dazu gibt es spaeter).  
  
> **ACHTUNG:** Im Domain-Projekt duerfen keine Aenderungen von Dateien mit dem Label ***@CodeCopy*** durchgefuehrt werden, da diesen beim naechsten Abgleich wieder ueberschrieben werden. Sollen dennoch Aenderungen vorgenommen werden, dann muss der Label ***@CodeCopy*** geaendert (z.B.: @CustomCode) oder entfernt werden. Damit wird diese Datei vom Abgleich mit der Vorlage ausgeschlossen.  
  
## Abgleich mit dem QuickTemplate  
  
In der Software-Entwicklung gibt es immer wieder Verbesserungen und Erweiterungen. Das betrifft die Vorlage ***QuickTemplate*** genauso wie alle anderen Projekte. Nun stellt sich die Frage: Wie koennen Verbesserungen und/oder Erweiterungen von der Vorlage auf die **Domain-Projekte** uebertragen werden?  
In der Vorlage sind die Quellcode-Dateien mit den Labels ***@BaseCode*** gekennzeichnet. Beim Kopieren werden diese Labels durch den Label ***@CodeCopy*** ersetzt. Mit dem Werkzeug **Comparison** im Programm **TemplateTools.ConApp** werden die Dateien mit dem Label ***@BaseCode*** und ***@CodeCopy*** abgeglichen. In der folgenden Skizze ist dieser Prozess dargestellt:  
  
![Template-Comparsion-Overview](TemplateComparsionOverview.png)  
  
Fuer den Abgleichprozess wird ebefalls die Werkzeugsammlung ***TemplateTools.ConApp*** verwendet:
  
```csharp
Template Tools
==============

Choose a tool:

[1] Copier..........Copy a quick template to a project
[2] Preprocessor....Setting defines for project options
[3] CodeGenerator...Generate code for template solutions
[4] Comparison......compares a project with the template and compares it
[x|X] Exit

Choose: 4
```
  
Nach der Bestaetigung der Auswahl erscheint die folgende Bildschirmmaske:
  
```csharp  
Template Comparison
===================

Balance label(s):
  @BaseCode       => @CodeCopy

Source: /Users/ggehrer/Projects/CSMacTemplate/QuickTemplate

[ +] Add path: ADD...
[ 1] Balancing for: /Users/ggehrer/Projects/Sample/QTMusicStoreLight
[ a] Balancing for: ALL...
[x|X...Quit]: 

Choose [n|n,n|x|X]: 1
```  
  
Wird nun die Option **[1 oder a]** aktiviert, dann werden alle Dateien in der Solution **QuickTemplate** mit der Kennzeichnung `@BaseCopy` mit den Dateien in der Solution  **QTMusicStoreLight** mit der Kennzeichnung `@CodeCopy` abgeglichen.  
  
## Setzen von Preprozessor-Defines  

Im Projekt ***QuickTemplate*** sind Preprozessor-Definitions definiert. Mit Hilfe dieser Definitions können Module und Funktionen  eingeschaltet bzw. ausgeschaltet werden. Diese *Definitions* werden natuerlich beim Kopieren in das Domain-Projekt uebernommen. Die folgende Tabelle bietet eine Uebersicht ueber die Module und Funktionen:

| Preprozessor-Definition | Modul/Funktion | Abhaengigkeit | Beschreibung |
|-------------------------|----------------|---------------|--------------|
|ACCOUNT_ON               | Authentifizierung| kein | Der Zugriff auf das System ist nur mit einen Konto gestattet. |
|LOGGING_ON               | Logging | ACCOUNT_ON | Die Manipultion der Daten wird mitprotokolliert. |
|REVISION_ON              | Historie | ACCOUNT_ON | Die Daten werden zusaetzlich in einer Historie verwaltet. |
|DEVELOP_ON               | Developer Mode | DEBUG | Zusaetzliche Funktionen wie Datenbank-Loeschen und Datenbank-Erstellen sind freigeschaltet. |  

```text  
Template Preprocessor
=====================

Definition-Values: ACCOUNT_OFF LOGGING_OFF REVISION_OFF DEVELOP_OFF

Set definition-values in 'QuickTemplate' from: ...\source\repos\HtlLeo\CSSoftwareEngineering\QuickTemplate

[1] Change source path
[2] Set definition ACCOUNT_ON
[3] Set definition LOGGING_ON
[4] Set definition REVISION_ON
[5] Set definition DEVELOP_ON
[6] Start assignment process...
[x|X] Exit

Choose:

```  

Wird eine Option **[2..6]** aktiviert, dann werden die Definitions fuer das ausgewaehlten Projekt gesetzt. Mit der Option **[1]** kann der entsprechende Pfad auf das Projekt geaendert werden.

# Umsetzungsschritte  
  
Nachdem nun das Domain-Projekt **QTMusicStoreLight** erstellt wurde, werden nun folgende Schritte der Reihenfolge nach ausgefuehrt:  
  
**Erstellen des Backend-Systems**  
  
- Erstellen der ***Enumeration***  
  - ...  
- Erstellen der ***Entitaeten***  
  - ...  
- Definition des ***Datenbank-Kontext***  
  - *DbSet&lt;Entity&gt;* definieren  
  - ...  
  - partielle Methode ***GetDbSet<E>()*** implementieren  
- Erstellen der ***Kontroller*** im *Logic* Projekt  
  - ***EntityController*** erstellen  
  - ...  
- Erstellen der ***Datenbank*** mit den Kommandos in der ***Package Manager Console***  
  - *add-migration InitDb*  
  - *update-database*  
- Implementierung der ***Business-Logic***  
- Erstellen des UnitTest-Projekt mit der Bezeichnung ***QTMusicStoreLight.Logic.UnitTest***  
  - Ueberpruefen der Geschaeftslogik mit ***UnitTests***  
- Importieren von Daten (optional)  
  
**Erstellen der AspMvc-Anwendung**  

Mit wenigen Schritte kann fuer das *Backend* eine AspMvc Web-Anwendung, fuer die Verwaltung und Bearbeitung von Daten, erstellt werden. Zu diesem Zweck sind die Schritte der Reihe nach auszufuehren:  

- Erstellen der Models  
  - ...  
- Erstellen der Kontroller  
  - ...  
- Erstellen der Ansichten  
  - ...  

> HINWEIS: Fuer die Erstellung der Ansichten (Views) koennen auch die bereitgestellten Standard-Ansichten (im Ordner /Views/Shared) verwendet werden. Eine Anleitung zur Verwendung dieser Ansichten befinden sich im Solution-Ordner *'Solution items'* mit dem Namen *'AspMvcDefaultViews.md'*.

**Erstellen des RESTful-Services**  
  
Um die Funktionen im Backend anderen (heterogenen) System zur Verfuegung zu stellen, ist es sinnvoll, dass diese Funktionalitaet ueber RESTful-Services delegiert werden.

- Erstellen der Models  
  - ...  
- Erstellen der Kontroller  
  - ...  
  
Die einzelnen Schritte sind im [Github-QTMusicStoreLight](https://github.com/leoggehrer/CSSoftwareEngineering-QTMusicStoreLight) detailiert aufgefuehrt.  
  
**Viel Spaß beim Umsetzen der Aufgabe!**  
