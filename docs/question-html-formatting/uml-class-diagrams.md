---
title: UML Class Diagrams
layout: default
parent: question.html Formatting
nav_order: 3
---

# UML Class Diagrams

To generate UML class diagrams that look neat and consistent every time, you can use the PlantUML syntax. Head over to [this website](https://editor.plantuml.com/uml/JO-n3i8m34HtVuN7Le14EtOgOc9XgSIU9XQrID8gSJk0-7VIL20yMDRptKdNHb51PcS11ZQ4ceEs1F71Vb91ETHMnNWI2TpFGXSz-ewVX4U0_C7pkg_A4Ru0q-ockRUiRoeqo5uoEqo15oMKOPUY_7tJ_ip5eaAL3NjCP_sLbPlEaGoZgOgoGJEcVFh7zOgNaGsy0Lho9hNv0000) which contains the following template in the editor pane:

```
@startuml

hide circle
skinparam classAttributeIconSize 0

class ClassName {
    +publicVar: int
    -privateVar: String
    +ClassName(var1: int, var2: String)
    +method1(): double
    +method2(): void
}

@enduml
```

From here, edit the fields so the preview pane on the right looks how it should.

If there are multiple classes, you can use syntax like this example to relate them. You can add as many classes and relationships as you want.

```
@startuml

hide circle
skinparam classAttributeIconSize 0

class A {
    fields
    methods()
}

class B {
    fields
    methods()
}

A <|-- B

@enduml
```

To export your UML class diagram, click the ![Image]({{ site.baseurl }}/assets/images/plantuml-png-export-icon.png) icon and save the image.

Inside the question folder, create a new folder called `clientFilesQuestion` if it does not already exist. Place the image into `clientFilesQuestion`, and insert this template into `question.html`, replacing `imagename.png` with the name of the image file:

```html
<pl-figure file-name="imagename.png" inline="true"></pl-figure>
```

The official documentation for PlantUML class diagrams can be found [here](https://plantuml.com/class-diagram), and the offical documentation for this question element can be found [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-figure-element).