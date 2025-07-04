# XML-basierte Logistikintegration zwischen Christian Carstensen Logistics & Dansk Distribution

> 🇬🇧 [English](README.en.md) | 🇩🇪 Deutsch | 🇩🇰 [Dansk](README.da.md)

## 🌍 Übersicht

Dieses Projekt demonstriert ein **produktionsreifes Datenaustauschsystem** auf Basis des **LisIn-XML-Formats** zwischen zwei Logistikunternehmen:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

### 🧪 Implementierungs-Highlights

Diese Lösung wurde in einer **hybriden Architektur** entwickelt:

* Die **ausgehende Schnittstelle** wurde von Anfang an vollständig in Python implementiert.
* Die **eingehende Integration** wurde zunächst gemäß Projektspezifikation mit dem **WinSped-Konverter 2.7** konzipiert und entwickelt. Während der Umsetzung stellte sich jedoch heraus, dass bestimmte Geschäftsregeln und Transformationen mit diesem Tool nicht abbildbar waren. Daher wurde die Eingangsverarbeitung schnell auf Python umgestellt, um Termine und technische Anforderungen einzuhalten.
* Die **Statusverarbeitung (Eingang)** wurde direkt in Python umgesetzt, um Monitoring, Erweiterbarkeit und Automatisierung zu erleichtern.
* Die **Statusrückmeldung (Ausgang)** ist derzeit in **VBS (Visual Basic Script)** realisiert, um schnelles Prototyping und einfache Geschäftslogik zu ermöglichen. Sobald alle dynamischen Regeln finalisiert sind, erfolgt die Migration nach Python.

### 🔢 Track & Trace Nummerngenerierung

Eindeutige T&T-Nummern werden über einen dateibasierten Zähler erzeugt:
```python
if len(TrackandTraceEmail) == 0:
    FBNR1 = str(FBNR_DEF())
    FBNR = '64500000'[:-len(FBNR1)] + FBNR1
```

Und die Zähler-Logik:
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

## 📦 Projektdateien

* `*_OL.xml` – Transportauftrag (OL)
* `*_OA.xml` – Beschaffungsauftrag (OA)
* `*_EJ.xml` – Teilstreckenauftrag (EJ)
* `Status_Codes.xml` – Statusmeldungen in 3 Sprachen

## 🧠 XML-Nachrichtenstrukturen

### 1. `OL_Distribution.xml` – Transportauftrag
```xml
<Order>
  <OrderID>OL20250704-001</OrderID>
  ...
</Order>
```

### 2. `OA_Beschaffung.xml` – Beschaffungsauftrag

* `Buyer`, `Supplier`, `OrderLines`, Lieferplan

### 3. `EJ_Teilstrecke.xml` – Teilstrecke

---

## 📨 Status_Codes.xml – Beschreibung

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

## 📊 Status-Codes-Tabelle

| Code | DE                                      | EN                              | DA                          |
|------|-----------------------------------------|----------------------------------|-----------------------------|
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

📄 Vollständige Liste in [`Status_Codes.md`](./Status_Codes.md)

## 🎯 Geschäftlicher Anwendungsfall

* **Automatische Schnittstelle**
* **Echtzeitsynchronisierung**
* **Lesbare Logs**

## 🔍 SEO-Optimierung

**Keywords**: XML Logistik-Schnittstelle, Freight API, LisIn, ERP-Anbindung, OCR + XML/JSON

## 📬 Kontakt

**Autor:** Alex Weiss – [LinkedIn](https://www.linkedin.com/in/alex-weiss-a6483417b)

> „Ich baue smarte Brücken zwischen Logistik, Daten und Menschen.“
