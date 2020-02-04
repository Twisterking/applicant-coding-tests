## Input

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<myRecipe version="lisa-stangl">
  <starter time="12:30">
    <dish>
      <name>Tomato Soup</name>
      <steps>
        <step count="1">Slice tomatoes</step>
        <step count="2">Slice vegetables</step>
        <step count="3">Boil water</step>
        <step count="4">Sauté vegetables, add tomatos later</step>
        <step count="5">Deglaze with white wine</step>
        <step count="6">Add water, let boil</step>
        <step count="7">Add seasoning</step>
        <step count="8">Enjoy</step>
      </steps>
    </dish>
  </starter>
  <mainCourse time="13:15">
    <dish>
      <name>Wiener Schnitzel</name>
      <steps>
        <step count="1">Beat the meat</step>
        <step count="2">
          <main>Bread the schnitzels</main>
          <substep>mix flour and salt, add eggs, add breadcrumbs</substep>
        </step>
        <step count="3">Heat oil in pan to 180 celsius</step>
        <step count="4">Fry the schnitzels</step>
        <step count="5">Serve and enjoy</step>
      </steps>
    </dish>
  </mainCourse>
</myRecipe>
```

## Pseudo Code:
```
var DATA = parseXML(<myRecipe/>)
var starter = {}
var mainCourse = {}

starter.NAME = DATA.starter.dish.name
starter.TIME = DATA.starter.$.time
starter.STEPS = []
FOR EACH step in DATA.starter.dish.steps DO
  ADD STEP TO starter.STEPS WITH
    COUNT = step.count AND
    TEXT = step.$

mainCourse.NAME = DATA.mainCourse.dish.name
mainCourse.TIME = DATA.mainCourse.$.time
mainCourse.STEPS = []
FOR EACH step in DATA.mainCourse.dish.STEPS DO
  ADD STEP TO mainCourse.steps WITH
    COUNT = step.count AND
    TEXT = step.$
    IF step.substep THEN
      TEXT = step.main AND
      SUBSTEP = step.substep

var dishes = [ starter, mainCourse ];
```
## Ergebnis:

#### Folgendes ist die Ausgabe von console.log(dishes) - also was ist der Inhalt der var "dishes" nach Ausführung von obigem Psuedo Code:

```js
dishes = [
  {
    NAME: "Tomate Soup",
    TIME: "12:30",
    STEPS: [
      { COUNT: 1, TEXT: "Slice tomatoes" },
      { COUNT: 2, TEXT: "Slice vegetables" },
      { COUNT: 3, TEXT: "Boil water" },
      { COUNT: 4, TEXT: "Sauté vegetables, add tomatos later" },
      { COUNT: 5, TEXT: "Deglaze with white wine" },
      { COUNT: 6, TEXT: "Add water, let boil" },
      { COUNT: 7, TEXT: "Add seasoning" },
      { COUNT: 8, TEXT: "Enjoy" },
    ]
  },
  {
    NAME: "Wiener Schnitzel",
    TIME: "13:15",
    STEPS: [
      { COUNT: 1, TEXT: "Beat the meat" },
      { COUNT: 2, TEXT: "Bread the schnitzels", SUBSTEP: "mix flour and salt, add eggs, add breadcrumbs" },
      { COUNT: 3, TEXT: "Heat oil in pan to 180 celsius" },
      { COUNT: 4, TEXT: "Fry the schnitzels" },
      { COUNT: 5, TEXT: "Serve and enjoy" },
    ]
  }
]
```
