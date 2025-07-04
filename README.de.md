# XML-basierte Logistik-Integration zwischen Christian Carstensen Logistics & Dansk Distribution

> 🇬🇧 [English](README.en.md) | 🇩🇪 [Deutsch](README.de.md) | 🇹🇼 [Dansk](README.da.md)

## 🌎 Überblick

Dieses Projekt zeigt ein **produktives Datenaustauschsystem** auf Basis des **LisIn XML-Formats** zwischen zwei Logistikunternehmen:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

Das System automatisiert:

* Transportauftragsübertragung (OL – Distribution)
* Beschaffungsauftragsschnittstelle (OA – Beschaffung)
* Teilstrecken-Anweisungen (EJ – Teilstrecke)
* Live-Statusübermittlung (90+ standardisierte Statuscodes)

---

## 📦 Projektdateien

* `OL_Distribution.xml` – Transportauftrag
* `OA_Beschaffung.xml` – Beschaffungsauftrag
* `EJ_Teilstrecke.xml` – Teilstreckenanweisungen
* `Status_Codes.xml` – Versandstatus in 3 Sprachen
* `Status_Codes.md` – 90+ mehrsprachige Statusbeschreibungen

---

## 🧠 XML-Struktur (basierend auf LisIn)

Alle Nachrichten folgen einem standardisierten LisIn XML-Schema:

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
      <GoodsDescription>Paletten</GoodsDescription>
      <Amount>12</Amount>
    </Position>
  </Positions>
</Order>
```

Varianten (OL, OA, EJ) enthalten geschäftsspezifische Felder.

---

## 📨 Status\_Codes.xml – Nachrichtenerklärung

Das Statusfile dokumentiert Transportereignisse als Code:

```xml
<StatusReport>
  <Status>
    <Code>6004</Code>
    <TextDE>Geleifert in LEMAN Trailer</TextDE>
    <TextEN>Delivered in LEMAN Trailer</TextEN>
    <TextDA>Leveret i Leman trailer</TextDA>
  </Status>
</StatusReport>
```

Die Codes sind mit realen Ereignissen verknüpft und branchenweit übertragbar.

---

## 📊 Statuscode-Tabelle

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

📅 Vollständige Liste siehe [`Status_Codes.md`](./Status_Codes.md)

---

## 🚀 Business-Use-Case

* **ERP Push**: Aufträge werden automatisch als XML gesendet
* **Webhook-Sync**: Statusmeldungen in Echtzeit
* **Lesbare Logs**: Für Disposition und Verwaltung

---

## 🔍 SEO-Schlüsselwörter

* XML Logistik-Schnittstelle, LisIn Standard, API Integration
* Frachtdaten Automatisierung, digitale Lieferkette
* Christian Carstensen Logistics, Dansk Distribution

---

## 📩 Kontakt

**Autor:** Alex Weiss – [LinkedIn Profil](https://www.linkedin.com/in/alex-weiss-a6483417b)

> „Ich baue smarte Brücken zwischen Logistik, Daten und Menschen.“

---

*Dieses Repository ist Teil meines professionellen Portfolios. Firmennamen dienen der technischen Veranschaulichung.*
