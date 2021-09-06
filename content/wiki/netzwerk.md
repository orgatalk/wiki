+++
title = "Netzwerk"
+++

Das Netzwerk gehört zu einem der Kernkomponenten einer LAN-Party. Umso wichtiger ist es ein stabiles Netzwerk aufzubauen, kleine Stolperfallen zu vermeiden und auch vor Fehlern der User gefeilt zu sein. Die Anforderungen sind aber je nach Gästegröße unterschiedlich sein. Hier sehen wir uns also mal eine Empfehlung an, die sich auf LAN-Partys bis 100 Leute gut umsetzen lässt.

## Der Backbone und die "richtige" Topologie

Als "Backbone" bezeichnet man das Bindeglied des kompletten Netzwerks. Jeder User muss irgendwie mit jedem User kommunzieren können. Zu alten BNC Zeiten war es ein Bus System. Das bedeutet die Daten hatten ein Anfang und sind einen Weg entlang gefahren. Mit der Einführung von Switches hat man sich für ein Sternsystem entschieden. Machen wir es mal an folgendem Beispiel:

Du hast vier Switche und drei Tischgruppen. Jede Tischgruppe möchtest du mit einem Switch ausstatten. Der optimale weg wäre also so, dass du Switch 1 in die "Mitte" stellt und jeweils ein Netzwerkkabel von Switch 1 an Switch 2, 3 und 4 anschließt, also eine Sterntopologie. Dieses Kabel nennt man dann auch "Uplink", denn dieses sorgt dafür auch mit den anderen Switchen kommunizieren zu können.
Jetzt könnte man noch auf die Idee kommen einen Ring zu bauen, sprich Switch 1 --> Switch 2, Switch 2 --> Switch 3, Switch 3 --> Switch 4, Switch 4 --> Switch 1. Kann man bauen, ist aber scheisse. Wieso? Weil mehere Uplinks für den Datentransfer genutzt werden müssen. Wir reden zwar im LAN über Milliesekunden, trotzdem stresst es ungeneim. 
Wir nehmen das Beispiel, dass ein User von Switch 2 mit Switch 4 sprechen möchte. Folgendes passiert:

 - Switch 2 nutzt seinen Uplink zu Switch 3
 - Das Paket geht dann weiter über den Uplink zu Switch 4

Bedeutet also wir haben zusätzlich noch den Uplink von Switch 3 belastet. Jetzt stellt euch mal vor alle User würden das machen, dann wären nicht nur die User an Switch 2 und Switch 4 in Leidenschaft, sondern auch an Switch 3. 

### Doppelt hält besser beim Uplink? Nicht unbedingt ...

Man könnte jetzt auf die Idee kommen, zwei Uplinks von Switch 1 zu Switch 2 zu bauen. Baut man dieses bei einem "dummen" Layer 2 Switch hat man erfolgreich einen Loop gebaut und hat gar kein funktionierendes Netzwerk mehr.

#### Ein Loop?
Richtig, der Tot eines jeden Netzwerk ist ein Loop. Dieses passiert z. B. wenn man ein Netzwerkkabel nimmt und beide Kabelenden an den selben Switch steckt, oder aber zwei Uplinks bauen möchte und keinen "Trunk" bauen kann. Macht man dass, weiß der Switch nicht genau, an welchen Port er das Paket adressieren soll weil er zwei ziele zur selben Adresse hat. Was dazu führt dann immer mehr Pakete verschickt werden und zur Überlastung des Switches sowie Netzwerkes.

## 100 Mbit/s vs. 1 Gbit/s vs. 10 Gbit/s
Es gab mal eine Zeit, da war 100 Mbit/s state of the art. Diese Zeiten sind schon lange vorbei, während 2,5 Gbit/s auf immer mehr Computer vorhanden ist kann man zu 99 % davon ausgehen heute mit 1 Gbit/s am PC ausgestattet zu sein. Wer heute also Hardware kauft (wenn sowas überhaupt noch neu vorhanden ist) kauft wirklich veraltete Technik. Spiele generell brauchen nicht viel Datenvolumen, wir sprechen da im Kilobyte pro Sekundebereich, trotzdem ist es nur von Vorteil einem User 1 Gbit/s anzubieten.

 - Oftmals ist der Uplink das 10-fache der typischen Portgeschwindigkeit. Wenn man sich also einen Tisch vorstellt mit 20 User, müssten 20 User sich 1 Gbit/s zum Backbone teilen. Dieses kann ganz schön eng werden.
 - Downloads von Patches, lokalen Steamcache usw. dauern im schlimmsten Fall 10 mal so lange, bedeutet 10 mal so lange Stress für den Uplink, dass den User selbst und auch die anderen Spieler am Tisch stören kann.

Dann gibt es noch 20 Gbit/s und 40 Gbit/s. Dieses sind Geschwindigkeiten, die nicht für den User bestimmt sind, sondern für den Uplink. 

## Uplink
Apropo Uplink: Von Vorteil ist es natürlich einen Uplinkport zu haben, der eben eine höhere Geschwindigkeit hat als ein User, ansonsten ist ein einziger User in der Lage, die Kommunikation aller anderen Teilnehmer am Tisch ganz schön zu stressen. Das führt dann zu Datenstau, einen höreren Ping, Lags uvm. Also alles Sachen, die gerade bei schnellen Shooter alles andere als schön ist.

## Layer-2 vs. Layer-3 Switche

### Layer 2

Diese Unterscheidung kommt aus dem OSI-Schicht Modell. Beim Layer-2 geht es darum, die Übertragung sicherzustellen z. B. durch Fehlerkorrekturen. Dabei passiert das einfach "stumpf" und es erfolgt keinerlei Flusskontrolle ob das Paket durch darf oder nicht. Sprich die Befehle, die der Switch bekommt setzt er einfach um ohne darüber nachzudenken, ob er das darf oder nicht.

### Layer 3
Beim Layer 3 gibt eine genaue Flusskontrolle. Bei den Switchen redet man auch von "managed Switches". Diese sind meistens über ein Web-Interface oder einer Kommandozeile konfigurierbar. Dort kann man dann genau festlegen, welcher Port darf was. Die Konfigurationsmöglichkeiten unterscheiden sich aber trotzdem auch bei jedem Hersteller und der Preiskategorie. Sind wir bei LAN-Partys von mehr als 100 Leuten unterwegs, ist es Pflicht einen Layer-3 Switch zu nehmen!

### Nimm ich also lieber managed Switche?

Dass kann man so pauschal nicht sagen. Klar ist, dass eine typische Keller-LAN mit 5 - 10 Teilnehmer so etwas nicht brauchen. Es gibt aber auch andere LANs mit knapp 100 Teilnehmer, die kein Layer-3 Switch haben, sei es entweder als finanziellen Gründen, oder sich die Konfigurations ersparen möchte.

## IP-Adresse
Die Computer im Netzwerk unterhalten sich über das IP-Protokoll. Sprich jeder Teilnehmer bekommt eine IP-Adresse und kann dann so mit anderen Computern reden.

### IP-Adressen Bereiche

Die Bereiche sind genau geregelt. So gibtes für interne Netzwerk drei IP-Bereiche nur man nutzen darf:

 - 10.0.0.0 - 10.255.255.255
 - 172.16.0.0 - 172.31.255.255
 - 192.168.0.0 - 192.168.255.255

### Netzmaske
Die Subnetzmaske gibt an, wie groß das eigene Netzwerk ist, jegliche Kommunikation außerhalb über ein Gateway erfolgen. Eine Angabe einer Subnetzmaske kann dabei in zwei Wegen erfolgen:

 - 10.0.0.0/8
 - 10.0.0.0 mit der Netzmaske 255.0.0.0

Im obengenannten Beispiel können jetzt 16.777.214 Computer eine IP-Adresse bekommen. Also ziemlich groß. Normale Heimrouter bieten meistens ein 192.168.0.0/24 Netz an, in diesem gibt es dann 255 Adressen. In welcher Größe ihr euer Netzwerk haben wollt müsst ihr entscheiden, wählt ihr es zu klein könnte es euch passieren das nicht alle Clients eine IP-Adresse bekommen. 

### Gateway

Das ist die Adresse, die genutzt wird um mit Netzen außerhalb eurem Netzwerk zu kommunizieren. Im Heimfall z. B. dann euer Router. 

## DHCP vs. non-DHCP
Um eine IP-Adresse zu erhalten gibt es zwei Wege:

 - Der Teilnehmer selbst trägt sich eine IP-Adresse über seine Systemsteuerung ein
 - Der Teilnehmer bekommt beim einstecken eine IP-Adresse zugewiesen

Das automatische Zuweisen der IP-Adresse erfolgt über eine DHCP-Server. Ob man einen DHCP-Server einsetzt oder nicht muss jeder selbst entscheiden, da streiten sich vorallem die Greister darüber.  Der vorteil eines DHCP Server ist ganz klar: Der User selbst muss nichts einstellen, er stöbselst sich einfach an den Netzwerkport und kann loszocken. Doch gerade in einem sehr großen Netzwerk jemand mit höheren Netzwerkkenntnissen so einiges an Schabernack anrichten, gerade wenn "nur" Layer-2 Switche im Einsatz sind!

### Bei DHCP gilt: first Come first Serve!
Man muss sich das mit DHCP so vorstellen: Sobald ein Client sich anstöbselt, brüllt er wie ein Affe: "HEY, ICH BIN HIER NEU UND BRAUCHE EINE IP-ADRESSE! WER HAT EINE FÜR MICH?". Und die erste Antwort die er darauf bekommt aktzeptiert er und bearbeitet sie. Genau dort liegt das Problem: Wenn sich in einem Netzwerk zwei DHCP-Server befinden kann dies übel enden, denn der zweite Server kann komplett andere Daten haben, somit können dann die Leute mit diesen zwei unterschiedlichen Netzen nicht miteinander kommunizieren. Bei einem Netzwerk mit Layer-3 Switchen kann dies unterbunden werden bzw. genau eingerichtet werden, welche IP-Adresse als DHCP-Server dienen darf. Wer jetzt aber aus dem Artikel herauslist gegen DHCP zu sein: Dem ist nicht so. Große sowie kleine LAN-Partys setzen auf DHCP-Server. Nur bei Layer-2 Netzwerken sollte man immer bereit sein mühsehlig den zu finden, der sich dachte auch IP-Adressen vergeben zu dürfen :) 

## Router
Die Kommunikation mit der Außenwelt (dieses Neuland namens Internet) sollte auch besser vorbereitet sein. Während eine Fritzbox ein Heimnetzwerk mit 10 - 20 Leuten noch so Meistern kann, würde es bei 100 Teilnehmern schon sehr eng werden. Von den fehlenden Konfigurationsmöglichkeiten mal abgesehen.

### Baut euch euren eigenen Router, auch Virtuell!

Der beste Weg ist es sich, für die Veranstaltung seinen eigenen Router zu bauen, dieser kann auch Virtuell sein! Alles was man dafür braucht ist min. zwei Netzwerkkarten (Eine fürs LAN-Netzwerk und jeweils eine für das WAN-Netzwerk [also das Internet]). Folgende Lösungen bieten sich für sowas zum Beispiel an:

 - [pfSense](https://www.pfsense.org)
 - [OPNSense](https://opnsense.org)
 - [IPFire](https://www.ipfire.org)
 - [Sophos XG](https://www.sophos.com/de-de/products/free-tools/sophos-xg-firewall-home-edition.aspx)

### Traffic shaping

Um was man nicht herumkommt ab einer gewissen Größe ist es den einzelnen Nutzer zu regulieren, wie viel Bandbreite er abgekommt. Fakt ist nunmal, die Verbindung ins Internet ist begrenzt und zwar stärker als im LAN. Ohne Beschränkungen wäre es also von einem User schon möglich mit einem etwas größeren Download die komplette Internetleitung zu blockieren und der gesamten LAN das Interneterlebnis vermiesen. Deshalb ist es wichtig zu sagen: Ein einziger User bekommt nur eine gewisse Bandbreite, da reichen selbst 128 kbit/s pro User. Wem das wenig vorkommt: Die meisten Spiele begnügen sich bereits mit ~ 50 kbit/s. 

### QoS

Ein weiterer Punkt der einem das Leben erleichten kann mit der Außenwelt ist Quality of Service (QoS). Damit kann man festlegen welche Datenpakete eine höhrere Priorität haben. QoS wird selbst im Heimrouter betrieben, jeder gängige Router weis, dass z. B. Datenpakete aus der Telefonie zeitkritisch und damit wichtiger sind als z. B. aus aufrufen einer Website. Das ist auch einer der Gründe für Lags wenn man einen großen Download hat. Ein Großteil des Datenverkehrs erfolgt über das TCP Protokoll, dass bei einem gesendeten Packet auf eine Bestätigung wartet. Im Beispiel eines großen Downloads ist es sehr oft so das auch der Upload komplett ausgelastet ist. Dies bedeutet dass das "ACK"-Paket, dass die Bestätigung für den richtigen Empfang des TCP-Paket ist, viel später ankommt, was zu einem höheren Ping und auch Lags führt.

