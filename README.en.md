# XML-based Logistics Integration Between Christian Carstensen Logistics & Dansk Distribution

> 🌎 [Deutsch](README.de.md) | [Dansk](README.da.md)

## 🌐 Overview

This project demonstrates a **production-ready data exchange system** based on the **LisIn XML format** between two logistics companies:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

The system automates:

* Transport order transfer (OL – Distribution)
* Purchase order interface (OA – Procurement)
* Sub-segment transport instructions (EJ – Partial Transport)
* Live status sharing (90+ standardized status codes)

---

## 📦 Project Files

* `OL_Distribution.xml` – Transport Order
* `OA_Beschaffung.xml` – Purchase Order
* `EJ_Teilstrecke.xml` – Sub-Segment Instructions
* `Status_Codes.xml` – Shipment Status Updates
* `Status_Codes.md` – 90+ multilingual status descriptions

---

## 🧠 XML Structure (LisIn-Based)

All documents follow a standard LisIn XML schema. Common structure:

```xml
<Order>
  <OrderID>123456</OrderID>
  <Sender>
    <Name>Christian Carstensen Logistics</Name>
    <GLN>9876543210001</GLN>
  </Sender>
  <Receiver>
    <Name>Dansk Distribution</Name>
    <GLN>1234567890001</GLN>
  </Receiver>
  <Positions>
    <Position>
      <GoodsDescription>Pallets</GoodsDescription>
      <Amount>12</Amount>
    </Position>
  </Positions>
</Order>
```

Variants (OL, OA, EJ) include unique business-specific fields.

---

## 📊 Status Codes

Status messages use numeric codes derived from LIS/EDIFACT. Example:

| Code | Status (EN)                     | Status (DE)                        | Status (DA)              |
| ---- | ------------------------------- | ---------------------------------- | ------------------------ |
| 1    | Handed over to external partner | Übergabe an externen Dienstleister | Overgivet til tredjepart |
| 2    | Hub outbound scan               | Hub Ausgang Scan                   | Transit - Lagerudgang    |
| 3    | Damage at departure             | Beschädigung bei Ausgang           | Skadet ved transit       |
| ...  | ...                             | ...                                | ...                      |

📅 See the full list in [`Status_Codes.md`](./Status_Codes.md)

---

## 🌟 Business Scenario

* **ERP Push**: Freight orders sent as XML from ERP
* **Webhook Sync**: Delivery statuses updated in real-time
* **Readable Logs**: For dispatch and operations staff

---

## 🔍 SEO Keywords

**English**:

* xml freight interface, lisin logistics, api integration
* transport data automation, digital supply chain
* Christian Carstensen Logistics, Dansk Distribution

---

## 📩 Contact

**Author:** Alex Weiss – [LinkedIn Profile](https://www.linkedin.com/in/alex-weiss-a6483417b)

> “I build smart bridges between logistics, data & humans.”

---

*This repository is part of my professional portfolio. Company names are used in a technical integration context.*
