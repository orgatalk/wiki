+++
title = "Netzwerk"
+++

Das Netzwerk ist einer der Kernkomponenten einer LAN-Party.
Umso wichtiger ist es, ein stabiles Netzwerk zu bieten, kleine Stolperfallen zu vermeiden und auch vor Fehlern der User gefeit zu sein.
Die Anforderungen sind aber je nach Anzahl der Teilnehmer unterschiedlich.
Hier sehen wir uns also mal eine Empfehlung an, die sich auf LAN-Partys bis 100 Leute gut umsetzen lässt.

## Der Backbone und die "richtige" Topologie

Als "Backbone" bezeichnet man das zentrale Bindeglied des kompletten Netzwerks.
Jeder User muss irgendwie mit jedem User kommunizieren können.
Zu BNC-Zeiten war es ein Bus-System.
Das bedeutet die Daten hatten ein Anfang und sind einen Weg entlang gefahren.
Mit der Einführung von Switches hat man sich für ein Sternsystem entschieden.
Machen wir es mal an folgendem Beispiel:

Du hast vier Switche und drei Tischgruppen.
Jede Tischgruppe möchtest du mit einem Switch ausstatten.
Der optimale weg wäre also so, dass du Switch 1 in die "Mitte" stellt und jeweils ein Netzwerkkabel von Switch 1 an Switch 2, 3 und 4 anschließt, also eine Sterntopologie.
Dieses Kabel nennt man dann auch "Uplink", denn dieses sorgt dafür auch mit den anderen Switchen kommunizieren zu können.
Jetzt könnte man noch auf die Idee kommen, einen Ring zu bauen, sprich Switch 1 → Switch 2, Switch 2 → Switch 3, Switch 3 → Switch 4, Switch 4 → Switch 1.
Kann man machen, ist aber scheiße.
Warum? Weil mehrere Uplinks für den Datentransfer genutzt werden müssen.
Wir reden zwar im LAN über Millisekunden, trotzdem stresst es ungemein.

Wir nehmen das Beispiel, dass ein User von Switch 2 mit Switch 4 sprechen möchte. Folgendes passiert:

 - Switch 2 nutzt seinen Uplink zu Switch 3.
 - Das Paket geht dann weiter über den Uplink zu Switch 4.

Bedeutet also, wir haben zusätzlich noch den Uplink von Switch 3 belastet.
Jetzt stellt euch mal vor, alle User würden das machen. Dann wären nicht nur die User an Switch 2 und Switch 4 in Leidenschaft, sondern auch an Switch 3.

### Doppelt hält besser beim Uplink? Nicht unbedingt …

Man könnte jetzt auf die Idee kommen, zwei Uplinks von Switch 1 zu Switch 2 zu bauen.
Baut man dieses bei einem "dummen" Layer-2-Switch, hat man erfolgreich einen Loop gebaut und hat gar kein funktionierendes Netzwerk mehr.

#### Ein Loop?

Richtig, der Tod eines jeden Netzwerk ist ein Loop.
Dieses passiert z.B., wenn man ein Netzwerkkabel nimmt und beide Kabelenden an den selben Switch steckt, oder aber zwei Uplinks bauen möchte und keinen "Trunk" bauen kann.
Macht man das, weiß der Switch nicht genau, an welchen der Ports er Pakete adressieren soll, weil er zwei Ziele zur selben Adresse hat.
Was dazu führt, dass immer mehr Pakete verschickt werden, und somit zur Überlastung des Switches sowie Netzwerkes.

## 100 Mbit/s vs. 1 Gbit/s vs. 10 Gbit/s
Es gab mal eine Zeit, da war 100 Mbit/s State of the Art.
Diese Zeiten sind schon lange vorbei. Während 2,5 Gbit/s auf immer mehr Computern vorhanden ist, kann man zu 99% davon ausgehen, heute mit 1 Gbit/s am PC ausgestattet zu sein.
Wer heute also Hardware kauft (wenn sowas überhaupt noch neu vorhanden ist), kauft wirklich veraltete Technik.
Spiele generell brauchen nicht viel Datenvolumen, wir sprechen da im Bereich Kilobyte pro Sekunde. Trotzdem ist es von Vorteil einem User 1 Gbit/s anzubieten.

 - Oftmals ist der Uplink das 10-fache der typischen Portgeschwindigkeit. Wenn man sich also einen Tisch mit 20 Usern vorstellt, müssten 20 User sich 1 Gbit/s zum Backbone teilen. Das kann ganz schön eng werden.
 - Downloads von Patches, lokalen Steamcache usw. dauern im schlimmsten Fall 10-mal so lange, bedeutet 10-mal so lange Stress für den Uplink, was den User selbst und auch die anderen Spieler am Tisch stören kann.

Dann gibt es noch 20 Gbit/s und 40 Gbit/s.
Dieses sind Geschwindigkeiten, die nicht für den User bestimmt sind, sondern für den Uplink.

## Uplink

Apropos Uplink: Von Vorteil ist es natürlich, einen Uplinkport zu haben, der eben eine höhere Geschwindigkeit hat als ein User, ansonsten ist ein einziger User in der Lage, die Kommunikation aller anderen Teilnehmer am Tisch ganz schön zu stressen.
Das führt dann zu Datenstau, einen höheren Ping, Lags u.v.m.
Also alles Sachen, die gerade bei schnellen Shootern alles andere als schön sind.

## Managed vs. Unmanaged Switches

### Unmanaged Switches

Ein nicht managebarer Switch ist die einfachste Form eines Switches.
Er macht einfach nur MAC-Address-Learning und leitet Pakete weiter.
Man kann den Switch einfach aufbauen und hoffen, dass er immer das richtige tut und sich auch alle Geräte im Netzwerk anständig verhalten.
Es gibt keinerlei Möglichkeiten, etwas zu konfigurieren oder zu überwachen.

### Managed Switches

Managebare Switches bieten viele Möglichkeiten, den Datenverkehr zu beeinflussen oder zu überwachen.
Dafür muss man das Gerät aber entsprechend konfigurieren.
Das passiert i.d.R. über ein Web-Interface, einen Console-Port oder per SSH.

Was das jeweilige Modell für Features unterstützt, steht im entsprechenden Datenblatt.
Öfter mal gebrauchen kann man:

- VLAN Tagging
- DHCP Snooping
- LACP/Port-Channels/LAGs (jeder Hersteller hat sich mal irgendwann gedacht, das Feature anders nennen zu müssen)
- SNMP
- Spanning-Tree-Protokol (am bestern RSTP oder MST)
- Access Controll Lists
- IGMP/MLD Snooping

### Nehm ich also lieber managed Switches?

Das kann man so pauschal nicht sagen.
Klar ist, dass eine typische Keller-LAN mit 5–10 Teilnehmern keine managed Switches braucht.
Managebare Switches bieten einen ganzen Haufen Features, die in vielen Situationen nützlich sein können.
Wer ein Netz aus unmanaged Switches betreibt, ist in vielen Fällen den Geräten im Netz hilflos ausgeliefert.
Mit managed Switches kann man zum einen sich gegen Probleme wie Loops oder Rogue DHCP Server schützen
und zum anderen genau herausfinden, an welchem Switchport ein gewisser Rechner hängt, wo der Loop gesteckt wurde,
ob ein Port viele kaputte Pakete empfängt, usw.
Falls man also die Wahl hat, möchte man sich für managebare Geräte entscheiden.
Die sind auch auf dem Gebrauchtmarkt relativ erschwinglich. Ansonsten kann man
einfach mal die freundliche LAN-Party in der Umgebung fragen, ob die einem
Geräte leihen können, weil bei denen liegt die Technik i.d.R. auch die meiste
Zeit vom Jahr im Keller.

## IP-Adresse

Die Computer im Netzwerk unterhalten sich über das IP-Protokoll.
Sprich, jeder Teilnehmer bekommt für den eigenen PC eine IP-Adresse und kann dann so mit anderen Computern kommunizieren.

### IP-Adressen Bereiche

Die Bereiche sind genau geregelt.
So gibt es für interne Netzwerk drei IP-Bereiche, die man nutzen darf:

- `10.0.0.0`–`10.255.255.255`
- `172.16.0.0`–`172.31.255.255`
- `192.168.0.0`–`192.168.255.255`

### Netzmaske

Die Subnetzmaske gibt an, wie groß das eigene Netzwerk ist. Jegliche Kommunikation außerhalb muss über ein Gateway erfolgen.
Die Angabe einer Subnetzmaske kann dabei auf zwei Arten erfolgen:

 - `10.0.0.0/8`
 - `10.0.0.0` mit der Netzmaske `255.0.0.0`

Im obengenannten Beispiel können jetzt 16.777.214 Computer eine IP-Adresse bekommen.
Also ziemlich groß.
Normale Heimrouter bieten meistens ein `192.168.0.0/24`-Netz an, in diesem gibt es dann 255 Adressen.
In welcher Größe ihr euer Netzwerk haben wollt müsst ihr entscheiden, wählt ihr es zu klein könnte es euch passieren das nicht alle Clients eine IP-Adresse bekommen.

### Gateway

Das ist die Adresse, die genutzt wird, um mit Netzen außerhalb eures Netzwerks zu kommunizieren.
Im Heimfall z. B. dann euer Router.

## DHCP vs. non-DHCP

Um eine IP-Adresse zu erhalten gibt es zwei Wege:

 - Der Teilnehmer selbst trägt sich eine IP-Adresse über seine Systemsteuerung ein
 - Der Teilnehmer bekommt beim einstecken eine IP-Adresse zugewiesen

Das automatische Zuweisen der IP-Adresse erfolgt über eine DHCP-Server.
Ob man einen DHCP-Server einsetzt oder nicht muss jeder selbst entscheiden, da streiten sich vor allem die Geister darüber.
Der Vorteil eines DHCP Server ist ganz klar: Der User selbst muss nichts einstellen, er stöpselst sich einfach an den Netzwerkport und kann loszocken.
Doch gerade in einem sehr großen Netzwerk jemand mit höheren Netzwerkkenntnissen so einiges an Schabernack anrichten, gerade wenn "nur" Layer-2-Switches im Einsatz sind!

### Bei DHCP gilt: first Come first Serve!

Man muss sich das mit DHCP so vorstellen: Sobald ein Client sich antobest, brüllt er wie ein Affe: "HEY, ICH BIN HIER NEU UND BRAUCHE EINE IP-ADRESSE! WER HAT EINE FÜR MICH?".
Und die erste Antwort die er darauf bekommt akzeptiert er und bearbeitet sie.
Genau dort liegt das Problem: Wenn sich in einem Netzwerk zwei DHCP-Server befinden kann dies übel enden, denn der zweite Server kann komplett andere Daten haben, somit können dann die Leute mit diesen zwei unterschiedlichen Netzen nicht miteinander kommunizieren.
Bei einem Netzwerk mit Layer-3 Switchen kann dies unterbunden werden bzw.genau eingerichtet werden, welche IP-Adresse als DHCP-Server dienen darf.
Wer jetzt aber aus dem Artikel herausliest gegen DHCP zu sein: Dem ist nicht so.
Große sowie kleine LAN-Partys setzen auf DHCP-Server.
Nur bei Layer-2 Netzwerken sollte man immer bereit sein mühselig den zu finden, der sich dachte auch IP-Adressen vergeben zu dürfen :)

## Router

Die Kommunikation mit der Außenwelt (dieses Neuland namens Internet) sollte auch besser vorbereitet sein.
Während eine Fritzbox ein Heimnetzwerk mit 10 - 20 Leuten noch so Meistern kann, würde es bei 100 Teilnehmern schon sehr eng werden.
Von den fehlenden Konfigurationsmöglichkeiten mal abgesehen.

### Baut euch euren eigenen Router, auch Virtuell!

Der beste Weg ist es sich, für die Veranstaltung seinen eigenen Router zu bauen, dieser kann auch virtuell sein! Alles, was man dafür braucht, sind mindestens zwei Netzwerkkarten (eine fürs LAN-Netzwerk und jeweils eine für das WAN-Netzwerk [also das Internet]).
Folgende Lösungen bieten sich für sowas zum Beispiel an:

 - [pfSense](https://www.pfsense.org)
 - [OPNSense](https://opnsense.org)
 - [IPFire](https://www.ipfire.org)
 - [Sophos XG](https://www.sophos.com/de-de/products/free-tools/sophos-xg-firewall-home-edition.aspx)

### Traffic Shaping

Um was man nicht herumkommt ab einer gewissen Größe ist es, den einzelnen Nutzer dahingehend zu regulieren, wie viel Bandbreite er abbekommt.
Fakt ist nun mal, die Verbindung ins Internet ist begrenzt und zwar stärker als im LAN.
Ohne Beschränkungen wäre es also von einem User schon möglich mit einem etwas größeren Download die komplette Internetleitung zu blockieren und der gesamten LAN das Interneterlebnis vermiesen.
Deshalb ist es wichtig zu sagen: Ein einziger User bekommt nur eine gewisse Bandbreite, da reichen selbst 128 kbit/s pro User.
Wem das wenig vorkommt: Die meisten Spiele begnügen sich bereits mit ~ 50 kbit/s.

### QoS

Ein weiterer Punkt der einem das Leben erleichtern kann mit der Außenwelt ist Quality of Service (QoS).
Damit kann man festlegen welche Datenpakete eine höhere Priorität haben.
QoS wird selbst im Heimrouter betrieben, jeder gängige Router weis, dass z. B. Datenpakete aus der Telefonie zeitkritisch und damit wichtiger sind als z. B. aus Aufrufen einer Website.
Das ist auch einer der Gründe für Lags, wenn man einen großen Download hat.
Ein Großteil des Datenverkehrs erfolgt über das TCP-Protokoll, dass bei einem gesendeten Paket auf eine Bestätigung wartet.
Im Beispiel eines großen Downloads ist es sehr oft so das auch der Upload komplett ausgelastet ist.
Dies bedeutet dass das "ACK"-Paket, dass die Bestätigung für den richtigen Empfang des TCP-Paket ist, viel später ankommt, was zu einem höheren Ping und auch Lags führt.
