> 🇬🇧 [English](README.en.md) | 🇩🇪 [Deutsch](README.de.md) | 🇩🇰 [Dansk](README.da.md)

# XML-based Logistics Integration Between Christian Carstensen Logistics & Dansk Distribution

## 🌍 Overview

This project demonstrates a **production-ready data exchange system** based on the **LisIn XML format** between two logistics companies:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

The system automates:

* Transport order transfer (OL – Distribution)
* Purchase order interface (OA – Beschaffung)
* Sub-segment transport instructions (EJ – Teilstrecke)
* Live status sharing with 90+ codes

---

## 📦 Project Files

* `OL_Distribution.xml` – Transport Order (OL)
* `OA_Beschaffung.xml` – Purchase Order (OA)
* `EJ_Teilstrecke.xml` – Sub-Segment Orders (EJ)
* `Status_Codes.xml` – Status Messages in 3 languages

---

## 🧠 Structure: XML Files (LisIn-Based)

All documents conform to a simplified `LisIn` schema. Here's a common layout:

```xml
<Order>
  <OrderID>...</OrderID>
  <Sender>
    <Name>Christian Carstensen Logistics</Name>
    <GLN>...</GLN>
  </Sender>
  <Receiver>
    <Name>Dansk Distribution</Name>
    <GLN>...</GLN>
  </Receiver>
  <Positions>
    <Position>
      <GoodsDescription>Pallets</GoodsDescription>
      <Amount>12</Amount>
    </Position>
  </Positions>
</Order>
```

Each variant (`OL`, `OA`, `EJ`) contains additional fields, depending on logistics step.

---

## 📊 Status Codes

Incoming and outgoing statuses (based on LIS/EDIFACT logic) reflect shipment stages:

| Code | Status (DE)                             | Status (EN)                     | Status (DA)                 |
| ---- | --------------------------------------- | ------------------------------- | --------------------------- |
| 1    | Übergabe an externen Dienstleister      | Handed over to external partner | Overgivet til tredjepart    |
| 2    | Hub Ausgang Scan                        | Hub outbound scan               | Transit - Lagerudgang       |
| 3    | Beschädigung bei Ausgang                | Damage at departure             | Skadet ved transit          |
| 4    | Geleifert in LEMAN Trailer              | Delivered into LEMAN trailer    | Leveret i LEMAN trailer     |
| 5    | Externer Dienstleister außerhalb DD     | External linehaul               | Ekstern linehaul            |
| 6    | Quittung auf Originalbeleg erforderlich | Original receipt required       | Originalkvittering påkrævet |
| 7    | Frachtbrief bereitgestellt              | Freight bill provided           | Fragtbrev klarmeldt         |
| 8    | Frachtbrief aktualisiert                | Freight bill updated            | Fragtbrev opdateret         |
| 9    | OMEX storniert                          | OMEX cancelled                  | Omex annulleret             |
| 10   | OMEX korrigiert                         | OMEX corrected                  | Omex rettet                 |
| ...  | ...                                     | ...                             | ...                         |

✅ Full list provided in `Status_Codes.md`

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
