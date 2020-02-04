## Beispiel Input:

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

```js
new variable DATA = parseXML(<myRecipe/>)
new variable starter
new variable mainCourse

starter.NAME = DATA.starter.dish.name
starter.TIME = DATA.starter.$.time
starter.STEPS = []
FOR EACH step IN DATA.starter.dish.steps DO
  ADD STEP TO starter.STEPS WITH
    COUNT = step.count AND
    TEXT = step.$

mainCourse.NAME = DATA.mainCourse.dish.name
mainCourse.TIME = DATA.mainCourse.$.time
mainCourse.STEPS = []
FOR EACH step IN DATA.mainCourse.dish.STEPS DO
  ADD STEP TO mainCourse.steps WITH
    COUNT = step.count AND
    TEXT = step.$
    IF step.substep THEN
      TEXT = step.main AND
      SUBSTEP = step.substep

new variable dishes
ADD starter TO dishes
ADD mainCourse TO dishes
```

## Beispiel Output:

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

## Aufgabe 1 (einfach)
<details>
  <summary>Ausklappen</summary>
  
  #### Finde die Fehler.
  Folgende Input-XML ist ähnlich der oberen, hat aber Fehler! Findest du alle Fehler?
  
  ## Finde die Fehler
  ```xml
  <?xml version="1.0" encoding="UTF-8" standalone="no" ?>
  <myRecipe versionn="lisa-stangl">
    <starter time="13:00"/>
      <name>Very fancy soup, but dangerous</name>
      <steps>
        <step count="1">Cook something something, this is a very long text.</step>
        <step count="2">Slice all the stuffs, maybe even cut some into dices - dices are fun!</step>
        <step count="3">Heat oil</step>
        <step count="4">
          Put water on it
          <substep>Very bad idea!</substep>
        </step>
        <step count="">Maybe die in the process ...</step>
        <step count="6">If still alive, enjoy</step>
      </steps>
      </myRecipe>
    </starter>
    <step></step>
    <mainCourse time="12:50">
      <name>Old School Schweinsbraten</name>
      <steps>
        <step>Prepare 'se meat and stuffs</step>
        <step substep="Has to be proper Waldviertler Erdäpfelknödel!">Make some Knödels</step>
        </step>
        <step>Make the Schweinsbraten ... da</step>
        <step>???</step>
        <step>Serve and enjoy</step>
      </steps>
  </myRecipe>
  ```
  
  <details>
    <summary>Schummeln und Fehler auflisten:</summary>
  
 * versionn
 * starter time ist VOR mainCourse
 * `<dish/>` Tag fehlt
 * Zwischen starter und mainCourse ist ein zusätzlicher step
 * myRecipe wird mitten drunter geschlossen
 * `<starter/>`:
   * starter Tag wird sofort wieder geschlossen (`<starter ...>` vs `<starter ... />`)
   * count fehlt bei step 5
   * step 4 fehlt der `<main/>` Tag
 * `<mainCourse/>`:
   * bei allen steps fehlt count
   * step 2 hat falsche syntax
   * step wird nach step2 2x geschlossen
   * mainCourse Tag wird niemals geschlossen
    
  </details>
</details>

## Aufgabe 2 (Mittel)
<details>
  <summary>Ausklappen</summary>
  
  #### ??? TODO

</details>

## Aufgabe 3 (schwer)
<details>
  <summary>Ausklappen</summary>

  #### Aufgabe ist es nun, mit dem Wissen aus obigem Beispiel Pseudo-Code zu schreiben, die aus folgendem Input folgenden Output produziert.

  ## Input:

  ```xml
  <?xml version="1.0" encoding="UTF-8" standalone="no" ?>
  <gastro:interchange xmlns:gastro="http://www.exite.at/xml/gastro/pricat2.0">
    <interchangeHeader>
      <interchangeSender>
        <mailboxID>9110017297940</mailboxID>
      </interchangeSender>
      <interchangeRecipient>
        <mailboxID>9110026029099</mailboxID>
      </interchangeRecipient>
      <interchangeIdentification>
        <uniqueCreatorIdentification>MDIQU000008831</uniqueCreatorIdentification>
      </interchangeIdentification>
      <interchangeCreationDateTime>2019-12-13T09:49:56</interchangeCreationDateTime>
      <applicationReference>PRICAT</applicationReference>
    </interchangeHeader>
    <priceCatalogue creationDateTime="2019-12-13T09:50:05" documentStatus="ORIGINAL" documentType="PRICAT">
      <pricatIdentification>
        <uniqueCreatorIdentification>PRICAT000008831</uniqueCreatorIdentification>
      </pricatIdentification>
      <pricatPartyIdentification>
        <seller>
          <gln>9110017297940</gln>
        </seller>
        <buyer>
          <gln>1000000000104</gln>
        </buyer>
      </pricatPartyIdentification>
      <pricatCurrency>
        <currencyISOCode>EUR</currencyISOCode>
      </pricatCurrency>
      <pricatLineItems>
        <pricatLineItem articleStatus="CHANGED" number="1" validityStartDate="2019-12-13">
          <tradeItemIdentification>
            <additionalTradeItemIdentification>
              <value>38</value>
              <type>SUPPLIER_ASSIGNED</type>
            </additionalTradeItemIdentification>
          </tradeItemIdentification>
          <itemDescription>
            <itemSpecificationCode>ORDERING_UNIT</itemSpecificationCode>
            <textLong>Radieschen VE 15 Bd.</textLong>
          </itemDescription>
          <priceInformation>
            <listPrice>
              <value>0.850</value>
              <calculationCode>NET_PRICE</calculationCode>
              <priceCode>DELIVERY</priceCode>
              <measurementUnitCodeValue>BD</measurementUnitCodeValue>
              <priceValidityStartDate>2019-12-14</priceValidityStartDate>
            </listPrice>
          </priceInformation>
          <packageInformation>
            <packageType>BD</packageType>
          </packageInformation>
          <foodRegulationInformation>
            <countryOfOrigin>IT</countryOfOrigin>
          </foodRegulationInformation>
        </pricatLineItem>
        <pricatLineItem articleStatus="CHANGED" number="199" validityStartDate="2019-12-13">
          <tradeItemIdentification>
            <additionalTradeItemIdentification>
              <additionalTradeItemIdentificationValue>3862</additionalTradeItemIdentificationValue>
              <additionalTradeItemIdentificationType>SUPPLIER_ASSIGNED</additionalTradeItemIdentificationType>
            </additionalTradeItemIdentification>
          </tradeItemIdentification>
          <itemDescription>
            <itemSpecificationCode>ORDERING_UNIT</itemSpecificationCode>
            <textLong>Möhren gelb  VE 10 kg</textLong>
          </itemDescription>
          <priceInformation>
            <listPrice>
              <value>1.350</value>
              <calculationCode>NET_PRICE</calculationCode>
              <priceCode>DELIVERY</priceCode>
              <measurementUnitCodeValue>KGM</measurementUnitCodeValue>
              <priceValidityStartDate>2019-12-14</priceValidityStartDate>
            </listPrice>
          </priceInformation>
          <packageInformation>
            <packageType>KGM</packageType>
          </packageInformation>
          <foodRegulationInformation>
            <countryOfOrigin>NL</countryOfOrigin>
          </foodRegulationInformation>
        </pricatLineItem>
        <pricatLineItem articleStatus="CHANGED" number="191" validityStartDate="2019-12-13">
          <tradeItemIdentification>
            <additionalTradeItemIdentification>
              <value>3636</value>
              <type>SUPPLIER_ASSIGNED</type>
            </additionalTradeItemIdentification>
          </tradeItemIdentification>
          <itemDescription>
            <itemSpecificationCode>ORDERING_UNIT</itemSpecificationCode>
            <textLong>Sprossen Alfalfa 100 g</textLong>
          </itemDescription>
          <priceInformation>
            <listPrice>
              <value>2.450</value>
              <calculationCode>NET_PRICE</calculationCode>
              <priceCode>DELIVERY</priceCode>
              <measurementUnitCodeValue>TA</measurementUnitCodeValue>
              <priceValidityStartDate>2019-12-14</priceValidityStartDate>
            </listPrice>
          </priceInformation>
          <packageInformation>
            <packageType>TA</packageType>
          </packageInformation>
          <foodRegulationInformation>
            <countryOfOrigin>NL</countryOfOrigin>
          </foodRegulationInformation>
        </pricatLineItem>
      </pricatLineItems>
    </priceCatalogue>
  </gastro:interchange>
  ```
  ## Pseudo Code:

  <details>
    <summary>Schummeln ;)</summary>
    
  ```js
  new variable DATA = parseXML(<gastro:interchange/>)
  new variable head
  new variable items

  head.SENDER = DATA.interchangeHeader.interchangeSender.mailboxID
  head.RECIPIENT = DATA.interchangeHeader.interchangeRecipient.mailboxID
  head.NAME = DATA.interchangeHeader.interchangeIdentification.uniqueCreatorIdentification
  head.DATETIME = DATA.interchangeHeader.interchangeCreationDateTime
  head.SELLER = DATA.priceCatalogue.pricatPartyIdentification.seller.gln
  head.BUYER = DATA.priceCatalogue.pricatPartyIdentification.buyer.gln

  FOR EACH pricatLineItem IN DATA.priceCatalogue.pricatLineItems DO
    ADD ITEM TO items WITH
      STATUS = pricatLineItem.$.articleStatus AND
      NUMBER = pricatLineItem.$.number AND
      REF = pricatLineItem.tradeItemIdentification.additionalTradeItemIdentification.value AND
      NAME = pricatLineItem.itemDescription.textLong AND
      PRICE = pricatLineItem.priceInformation.listPrice.value AND
      UNIT = pricatLineItem.packageInformation.packageType AND
      ORIGIN = pricatLineItem.foodRegulationInformation.countryOfOrigin
  ```
  </details>

  ## Gewünschter Output:

  ```js
  head = {
    SENDER: "9110017297940",
    RECIPIENT: "9110026029099",
    NAME: "MDIQU000008831",
    DATETIME: "2019-12-13T09:49:56",
    SELLER: "9110017297940",
    BUYER: "1000000000104"
  }
  items = [
    {
      STATUS: "CHANGED",
      NUMBER: "1",
      REF: "38",
      NAME: "Radieschen VE 15 Bd.",
      PRICE: "0.850",
      UNIT: "BD",
      ORIGIN: "IT"
    },
    {
      STATUS: "CHANGED",
      NUMBER: "199",
      REF: "3862",
      NAME: "Möhren gelb  VE 10 kg",
      PRICE: "1.350",
      UNIT: "KGM",
      ORIGIN: "NL"
    },
    {
      STATUS: "CHANGED",
      NUMBER: "191",
      REF: "3636",
      NAME: "Sprossen Alfalfa 100 g",
      PRICE: "2.450",
      UNIT: "TA",
      ORIGIN: "NL"
    }
  ]
  ```
</details>
