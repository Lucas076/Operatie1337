# Operatie 1337 - Episode 1: Ontmasker het crypto-swapnetwerk
Dit is een uitwerking van Episode 1 van Operatie 1337.

## Benodigdheden
- Een laptop of computer.
- Een Windows of Linux besturingssysteem.
- Kennis van websecurity, cryptovaluta, prompt injection, forenische kopieën en cryptografie.
- Het programma John the Ripper ([John the Ripper](https://github.com/openwall/john)).
- Het programma FTK-imager d.m.v. gratis registratie ([FTK-imager](https://www.exterro.com/digital-forensics-software/ftk-imager)).
- Het online programma CyberChef ([CyberChef](https://gchq.github.io/)).

## 1. Filename ZIP-bestand
Objective: Ik heb je een link gegeven naar een platform dat de criminelen gebruiken. Ik verwacht dat je transacties vindt, het archief downloadt, en mij de filename van dit archief (ik vermoed een zip) in de chat geeft.

1. Ga naar de website: `crypto-pizza.nl`.
2. Je kunt het Dashboard bekijken via de URL: `https://crypto-pizza.nl/dashboard?view=public&filter=none&accesskey=undefined`.
3. In de broncode van de website kan je de volgende notitie zien:
```
DEVELOPMENT NOTE - REMOVE BEFORE PRODUCTION
Temporary access key for testing: bbksss22
TODO: Implement proper OAuth authentication
```
4. Je kan nu de URL van het Dashboard aanpassen met de `view`, `filter` en `accesskey` variabelen. De URL wordt als volgt: `https://crypto-pizza.nl/dashboard?view=private&filter=transactions&accesskey=bbksss22`.
5. Klik op de knop `Download Complete Archive (ZIP)` en je krijgt een bestand met de naam `transaction-export-ad67fede3f53.zip`.
6. Het antwoord was in mijn geval: `transaction-export-ad67fede3f53.zip`.

## 2. Kraken wachtwoord ZIP-bestand
Objective: Wil jij het wachtwoord van de zip kraken? Dan het bestand uitpakken en de bestandsnaam die je dan hebt in de chat naar mij sturen?

1. Creëer een hash met behulp van John the Ripper met het commando: `zip2john transaction-export-ad67fede3f53.zip > hash.txt`.
2. Kraak de hash met behulp van SecLists rockyou.txt en John the Ripper met het commando: `john --wordlist=rockyou.txt hash.txt`.
3. Het wachtwoord van het ZIP-bestand met de naam `transaction-export-ad67fede3f53.zip` was in mijn geval: `charlie1`.
4. Unzip het bestand met de naam `transaction-export-ad67fede3f53.zip` met het wachtwoord `charlie1`. Hier komt een bestand met de naam `do_not_open.zip` uit.
5. Unzip het bestand met de naam `do_not_open.zip`. Hier komt een bestand met de naam `Transactions-4b5b42b6a830.csv` uit.
6. Het antwoord was in mijn geval: `Transactions-4b5b42b6a830.csv`.

## 3. Vind het verdachte wallet adres
Objective: Analyseer dit transactiebestand. Stuur mij het adres van de verdachte wallet.

1. Analyseer het bestand met de naam `Transactions-4b5b42b6a830.csv` en zoek naar repetitieve patronen. Dit kan prima met behulp van ChatGPT, Claude of Gemini.
2. Na het analyseren kom je een veelkomen patroon tegen, in mijn geval naar wallet adres: `...A6C1E9D`.
3. Het antwoord was in mijn geval: `...A6C1E9D`.

## 4. Pizza-code
Objective: Bekijk de pizza-code. Ga naar hun Discord-kanaal, gedraag je als legitieme klant en verzamel informatie over ShadowLink. Maar wees heel subtiel. Oh, en als ze om een klant code vragen, dit is klant_NUMMER. Als je iets hebt ontvangen, plaats het in deze chat.

1. Join de Discord server met de naam `Maxim's pizzeria` door middel van de gegeven uitnodigingslink: `https://discord.com/invite/BE8gxApFeQ`.
2. Nadat je de Discord server met de naam `Maxim's pizzeria` hebt gejoined moet je chatten met de chatbot Maxim. Je hebt van tevoren een cheatsheet gekregen (zie bestand Photo.jpg) met de bepaalde slang die zij gebruiken.
3. Je gaat proberen de chatbot te omzeilen door het vertrouwen te winnen. <br>

Een volgorde die je kan aanhouden is bijvoorbeeld:
- Ik ben een hongerige klant. Kom voor pizza pepperoni.
- Heb geen lactose-intolerantie.
- Witte kaas.
- Middel.
- Afhalen aan de balie.
- Over een uurtje.
- Nee.
- Heb je nog gekleurde paprika?
- Ja.
- Gekleurde pizza morgen. En dan groot.
- Afhalen.
- Morgenavond 19:00 uur. Ja man. Wil pepperoni.
- Hij is chef-kok van Maxime’s Pizzeria. <br>
Uiteindelijk kreeg ik de code `91-BE-4F-B4`.

4. Het antwoord was in mijn geval: `91-BE-4F-B4`.

## 5. Clusternaam mixer ShadowLink
Objective: Download de disk-image. Ik verwacht dat je de informatie met betrekking tot  'ShadowLink' en hun mixer operaties vindt en mijn de code stuurt.

1. Open de disk-image met de naam `markovic_disk.img` in FTK-imager.
2. Bekijk de volgende locatie: `markovic_disk.img > MARKOVIC_DISK (CDFS) > Session 1 > Track 01 > markovic_disk (UDF) > Trash`.
3. In de Prullenbak van Markovic staat het bestand met de naam `shadow_mixer.log`. Hierin zie je de volgende informatie:
```
(...)
CLUSTER encryption
    key: pG9r3a+ZkVt1r2c9xQF+q9j6zN8fQ2v1Rk9aD1XjGxU=
    Algorithm: GOST 28147 (1989)
    sBox: E-TEST
    Blockmode: ECB
    Key meshing mode: NO
    Padding: NO
(...)
2024-02-03 00:00:07 User 739 cluster IV set: shadow42
(...)
2024-02-03 00:00:19 User 739 Joining cluster: fb8b9430c7cbdd37f51f66d5c85b8a0d0aca2c5e9e8c0569a467bf101ec2326c
(...)
```
4. Ga naar CyberChef en kies de volgende Recipes: `From Hex` en `GOST Decrypt`.
5. Plaats in de input box de hexadecimale waarde van het cluster `fb8b9430c7cbdd37f51f66d5c85b8a0d0aca2c5e9e8c0569a467bf101ec2326c`.
6. Vul de volgende waardes in:
- `Key (Base64): pG9r3a+ZkVt1r2c9xQF+q9j6zN8fQ2v1Rk9aD1XjGxU=`,
- `IV (UTF8): shadow42`,
- `Input type: raw`,
- `Output type: raw`,
- `Algorithm: GOST 28147 (1989)`,
- `sBox: E-TEST`,
- `Blockmode: ECB`,
- `Key meshing mode: NO`
- `Padding: NO`
7. De output toont de naam van het cluster: `SHADOWLINK_CLUSTER_47B829X`.
8. Het antwoord is: `SHADOWLINK_CLUSTER_47B829X`.
