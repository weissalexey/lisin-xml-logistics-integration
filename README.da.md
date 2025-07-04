# XML-baseret logistik-integration mellem Christian Carstensen Logistics & Dansk Distribution

> 🇬🇧 [English](README.en.md) | 🇩🇪 [Deutsch](README.de.md) | 🇩🇰 [Dansk](README.da.md)

## 🌍 Oversigt

Dette projekt demonstrerer et **produktionsklart dataudvekslingssystem** baseret på **LisIn XML-formatet** mellem to logistikvirksomheder:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

Systemet automatiserer:

* Transportordreoverførsel (OL – Distribution)
* Indkøbsordregrænseflade (OA – Beschaffung)
* Delstrækningstransportinstruktioner (EJ – Teilstrecke)
* Live statusdeling med 90+ koder (Status XML)

---

## 📦 Projektfiler

* `OL_Distribution.xml` – Transportordre (OL)
* `OA_Beschaffung.xml` – Indkøbsordre (OA)
* `EJ_Teilstrecke.xml` – Delstrækningsinstruktioner (EJ)
* `Status_Codes.xml` – Statusmeddelelser på 3 sprog

---

## 🧠 XML-meddelelsesstrukturer

### 1. OL\_Distribution.xml – Transportordre

Denne meddelelse indeholder forsendelsesinstruktioner:

```xml
<Order>
  <OrderID>OL20250704-001</OrderID>
  <Sender>
    <Name>Christian Carstensen Logistics</Name>
    <GLN>1234567890123</GLN>
  </Sender>
  <Receiver>
    <Name>Dansk Distribution</Name>
    <GLN>9876543210987</GLN>
  </Receiver>
  <Delivery>
    <Date>2025-07-05</Date>
    <Address>
      <Street>Transportvej 12</Street>
      <PostalCode>4000</PostalCode>
      <City>Roskilde</City>
      <Country>DK</Country>
    </Address>
  </Delivery>
  <Positions>
    <Position>
      <ItemCode>PALLET_001</ItemCode>
      <Description>Europaller med varer</Description>
      <Quantity>12</Quantity>
      <Weight>960</Weight>
    </Position>
  </Positions>
</Order>
```

### 2. OA\_Beschaffung.xml – Indkøbsordre

Beskriver planlagte indkøb fra leverandørnetværk. Indeholder:

* `Buyer`
* `Supplier`
* `OrderLines`
* Leveringsplan

### 3. EJ\_Teilstrecke.xml – Delstrækning

Bruges til at forbinde langdistance med last-mile partnere.

---

## 📨 Status\_Codes.xml – Beskrivelse af meddelelse

Statusfilen bruger kompakte poster til at spore transportlivscyklus:

```xml
<StatusReport>
  <Status>
    <Code>6004</Code>
    <TextDE>Geleifert in LEMAN Trailer</TextDE>
    <TextEN>Delivered in LEMAN Trailer</TextEN>
    <TextDA>Leveret i LEMAN trailer</TextDA>
  </Status>
  <!-- +90 poster -->
</StatusReport>
```

Koderne svarer til virkelige hændelser og er harmoniseret på tværs af netværk.

---

## 📊 Statustabeller

| Kode | DE                                  | EN                              | DA                       |
| ---- | ----------------------------------- | ------------------------------- | ------------------------ |
| 1    | Übergabe an externen Dienstleister  | Handed over to external partner | Overgivet til tredjepart |
| 2    | Hub Ausgang Scan                    | Hub outbound scan               | Transit - Lagerudgang    |
| 3    | Beschädigung bei Ausgang            | Damage at departure             | Skadet ved transit       |
| 4    | Geleifert in LEMAN Trailer          | Delivered in LEMAN trailer      | Leveret i LEMAN trailer  |
| 5    | Externer Dienstleister außerhalb DD | External linehaul               | Ekstern linehaul         |
| ...  | ...                                 | ...                             | ...                      |

📄 Fuld liste i [`Status_Codes.md`](./Status_Codes.md)

---

## 🎯 Forretningsbrug

* **Automatiseret grænseflade**: One-click XML push fra ERP
* **Live synkronisering**: Statusopdateringer via webhook
* **Læsbare logfiler** til operatører og disponenter

---

## 🔍 SEO-optimering (Engelsk / Tysk / Dansk)

**Søgeord**:

* XML logistikgrænseflade / XML Logistik-Schnittstelle / XML logistics interface
* freight API, LisIn format, ERP integration
* OCR + dataudveksling (JSON/XML/PDF)

---

## 📬 Kontakt

**Forfatter:** Alex Weiss – [LinkedIn](https://www.linkedin.com/in/alex-weiss-a6483417b)

Denne repo er en del af min offentlige portefølje og kan bruges som model for fremtidige LisIn-baserede projekter.

> "Jeg bygger smarte broer mellem logistik, data og mennesker."

*Alle virksomhedsnavne bruges som professionelle referencer.*
