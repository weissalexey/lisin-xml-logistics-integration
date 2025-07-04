# XML-baseret logistik-integration mellem Christian Carstensen Logistics & Dansk Distribution

> 🇬🇧 [English](README.en.md) | 🇩🇪 [Deutsch](README.de.md) | 🇩🇰 Dansk

## 🌍 Oversigt

Dette projekt demonstrerer et **produktionsklart dataudvekslingssystem** baseret på **LisIn XML-formatet** mellem to logistikvirksomheder:

* [Christian Carstensen Logistics](https://www.carstensen.eu)
* [Dansk Distribution](https://www.danskdistribution.dk)

### 🧪 Implementeringshøjdepunkter

Løsningen er udviklet i en **hybridarkitektur**:

* Den **udgående grænseflade** blev fra starten implementeret fuldt ud i Python.
* Den **indgående integration** blev oprindeligt defineret og udviklet med **WinSped-Konverter 2.7**, i henhold til projektspecifikationerne. Under udviklingen blev det dog klart, at visse forretningsregler og transformationer ikke var mulige inden for rammerne af dette værktøj. Derfor blev indløbsrøret hurtigt genimplementeret i Python for at opfylde tidsplan og tekniske krav.
* **Statusmodtagelse** (livscyklusbegivenheder fra partneren) blev straks bygget i Python for nem overvågning, fleksibilitet og automatisering.
* **Statuseksport** (feedback til partneren) er i øjeblikket implementeret i **VBS (Visual Basic Script)** for hurtig iteration og enkel logiktilføjelse. Denne del vil senere blive migreret til Python, når al dynamisk logik er fastlagt.

### 🔢 Track & Trace-nummergenerering

Unikke T&T-numre oprettes ved hjælp af en filbaseret tæller:

```python
if len(TrackandTraceEmail) == 0:
    FBNR1 = str(FBNR_DEF())
    FBNR = '64500000'[:-len(FBNR1)] + FBNR1
```

Tællerlogikken:

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

## 📦 Projektfiler

* `*_OL.xml` – Transportordre (OL)
* `*_OA.xml` – Indkøbsordre (OA)
* `*_EJ.xml` – Delstrækningsordre (EJ)
* `Status_Codes.xml` – Statusmeddelelser på 3 sprog

---

## 🧠 XML-meddelelsesstruktur

### 1. `OL_Distribution.xml` – Transportordre
```xml
<Order>
  <OrderID>OL20250704-001</OrderID>
  ...
</Order>
```

### 2. `OA_Beschaffung.xml` – Indkøbsordre

* `Buyer`, `Supplier`, `OrderLines`, leveringsplan

### 3. `EJ_Teilstrecke.xml` – Delstrækning

---

## 📨 Status_Codes.xml – Beskrivelse

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

## 📊 Statuskoder-tabel

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

📄 Fuld liste i [`Status_Codes.md`](./Status_Codes.md)

## 🎯 Forretningsbrug

* **Automatiseret grænseflade**
* **Synkronisering i realtid**
* **Læsbare logfiler**

## 🔍 SEO-optimering

**Keywords**: XML logistikgrænseflade, freight API, LisIn, ERP-integration, OCR + XML/JSON

## 📬 Kontakt

**Forfatter:** Alex Weiss – [LinkedIn](https://www.linkedin.com/in/alex-weiss-a6483417b)

> "Jeg bygger smarte broer mellem logistik, data og mennesker."
