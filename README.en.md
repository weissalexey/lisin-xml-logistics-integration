# XML-based Logistics Integration Between Christian Carstensen Logistics & Dansk Distribution

> 🇬🇧 [English](README.en.md) | 🇩🇪 [Deutsch](README.de.md) | 🇩🇰 [Dansk](README.da.md)

## 🌍 Overview

This project demonstrates a **production-ready data exchange system** based on the **LisIn XML format** between two logistics companies:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

### 🧪 Implementation Highlights

This solution was developed in a **hybrid architecture**:

* The **outbound interface** was implemented fully in Python from the start.
* Initially, the **inbound integration** was scoped and developed with **WinSped-Konverter 2.7**, as per project specification. However, during development, it became evident that certain business rules and transformations were not feasible within the limitations of that tool. As a result, the inbound pipeline was rapidly reimplemented in Python to meet deadline and technical requirements.
* The **status intake** (receiving lifecycle events from the partner) was built on Python immediately to enable easy monitoring, extensibility, and automation.
* The **status export** (feedback from our side to the partner) is currently implemented in **VBS (Visual Basic Script)** for quick iteration and simplicity of business logic insertion. Once all dynamic logic is finalized, this portion will also be migrated to Python.

### 🔢 Track & Trace Number Generation

Unique T\&T numbers are created using a file-based counter:

```python
if len(TrackandTraceEmail) == 0:
    FBNR1 = str(FBNR_DEF())
    FBNR = '64500000'[:-len(FBNR1)] + FBNR1
```

And the counter logic:

```python
def FBNR_DEF():
    COUNT_FILE = os.path.join('//srv-wss/Schnittstellen/DansckDistribution/FBNR.COUNTER')
    if not os.path.exists(COUNT_FILE):
        num = 0
    else:
        f = open(COUNT_FILE, 'r')
        num = int(f.read())
        f.close()
    FBB = str(num)
    num += 1
    f = open(COUNT_FILE, 'w')
    f.write(str(num))
    f.close()
    return FBB
```

---

## 📦 Project Files

* `_OL.xml` – Transport Order (OL)
* `_OA.xml` – Purchase Order (OA)
* `_EJ.xml` – Sub-Segment Orders (EJ)
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
