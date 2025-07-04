# XML-based Logistics Integration Between Christian Carstensen Logistics & Dansk Distribution

> 🇬🇧 [English](README.en.md) | 🇩🇪 [Deutsch](README.de.md) | 🇩🇰 [Dansk](README.da.md)

## 🌍 Overview

This project demonstrates a **production-ready data exchange system** based on the **LisIn XML format** between two logistics companies:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

The system automates:

* Transport order transfer (OL – Distribution)
* Purchase order interface (OA – Beschaffung)
* Sub-segment transport instructions (EJ – Teilstrecke)
* Live status sharing with 90+ codes (Status XML)

---

## 📦 Project Files

* `OL_Distribution.xml` – Transport Order (OL)
* `OA_Beschaffung.xml` – Purchase Order (OA)
* `EJ_Teilstrecke.xml` – Sub-Segment Orders (EJ)
* `Status_Codes.xml` – Status Messages in 3 languages

---

## 🧠 XML Message Structures

### 1. OL\_Distribution.xml – Transport Order

This message contains shipment-level instructions:

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
      <Description>Europallets with goods</Description>
      <Quantity>12</Quantity>
      <Weight>960</Weight>
    </Position>
  </Positions>
</Order>
```

### 2. OA\_Beschaffung.xml – Purchase Order

Describes planned purchases from supplier networks. It includes:

* `Buyer`
* `Supplier`
* `OrderLines`
* Delivery schedule

### 3. EJ\_Teilstrecke.xml – Sub-segment

Used for linking long-haul with last-mile partners.

---

## 📨 Status\_Codes.xml – Message Description

The status file uses compact entries for tracking transport lifecycle:

```xml
<StatusReport>
  <Status>
    <Code>6004</Code>
    <TextDE>Geleifert in LEMAN Trailer</TextDE>
    <TextEN>Delivered in LEMAN Trailer</TextEN>
    <TextDA>Leveret i Leman trailer</TextDA>
  </Status>
  <!-- +90 entries -->
</StatusReport>
```

The `Code` corresponds to real-world events, many of which are harmonized across freight networks.

---

## 📊 Status Codes Table

| Code | DE                                      | EN                              | DA                          |
| ---- | --------------------------------------- | ------------------------------- | --------------------------- |
| 1    | Übergabe an externen Dienstleister      | Handed over to external partner | Overgivet til tredjepart    |
| 2    | Hub Ausgang Scan                        | Hub outbound scan               | Transit - Lagerudgang       |
| 3    | Beschädigung bei Ausgang                | Damage at departure             | Skadet ved transit          |
| 4    | Geleifert in LEMAN Trailer              | Delivered in LEMAN trailer      | Leveret i LEMAN trailer     |
| 5    | Externer Dienstleister außerhalb DD     | External linehaul               | Ekstern linehaul            |
| 6    | Quittung auf Originalbeleg erforderlich | Original receipt required       | Originalkvittering påkrævet |
| 7    | Frachtbrief bereitgestellt              | Freight bill provided           | Fragtbrev klarmeldt         |
| 8    | Frachtbrief aktualisiert                | Freight bill updated            | Fragtbrev opdateret         |
| 9    | OMEX storniert                          | OMEX cancelled                  | Omex annulleret             |
| 10   | OMEX korrigiert                         | OMEX corrected                  | Omex rettet                 |
| ...  | ...                                     | ...                             | ...                         |

📄 Full list in [`Status_Codes.md`](./Status_Codes.md)

---

## 🎯 Business Use Case

* **Automated interface:** One-click XML push from ERP to API
* **Real-time sync:** Status updates pushed via webhook
* **Human-readable logs** for dispatchers and operations

---

## 🔍 SEO Optimization (English / German / Danish)

**Keywords**:

* XML logistics interface / XML Logistik-Schnittstelle / XML logistikgrænseflade
* freight API, LisIn format, freight automation
* ERP connection for logistics (LISIN, A4L, Spedion)
* OCR + JSON/XML/PDF data exchange

---

## 📬 Contact

**Author:** Alex Weiss – [LinkedIn](https://www.linkedin.com/in/alex-weiss-a6483417b)

You can use this structure to build your own **LisIn-based logistics bridge** between any two carriers or partners.

> “I build smart bridges between logistics, data & humans.”

---

*Repository is part of my public portfolio. All company names are used with professional reference.*
