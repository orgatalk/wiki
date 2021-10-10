+++
title = "Gameserver"

[extra]
authors = ["Y0Gi"]
+++

Multiplayer-Spiele nach dem [Client-Server-Prinzip](https://de.wikipedia.org/wiki/Client-Server-Modell)
haben üblicherweise einen Host, der die Koordination des Mehrspielergeschehens übernimmt und die Autorität für das
für alle Clients geltende Geschehen ist.

Die Rolle des Host können dabei unterschiedliche Programme übernehmen.


# Listen Server

Kann aus einem zum Spielen installierten Spiele-Client heraus ein eigener Server angeboten werden, dem andere Clients
(zumindest im selben [Netzwerk](/wiki/netzwerk)) beitreten können, so spricht man von einem "Listen Server".

Dies bedarf keiner zusätzlichen Software und Konfiguration. Es gibt jedoch Nachteile:

- Der Host muss sich die Ressourcen des Computers mit der Darstellung des Spiels teilen. Kommt der Rechner an Grenzen,
  kann sich das negativ auf das gemeinsame Spielgeschehen auswirken und bspw. zu störenden Aussetzern führen.

- Je nach Spiel und Netzwerk kann für den Client, der den Host stellt, ein spielerischer Vorteil gegenüber den anderen
  Clients bestehen, weil dieser "näher an der Quelle" ist und z. B. schneller reagieren kann bzw. die eigenen Aktionen
  eher vom Host empfangen werden.


# Dedicated Server

Ein Dedicated Server ist eine separate Applikation, die nur die Host-Funktion eines Spiels übernimmt, aber das Spiel
nicht in Form von Bild und Ton darstellt.

Dadurch kann sie auf einem Server ohne grafische Benutzungsoberfläche und an anderer Stelle im Netzwerk betrieben
werden. Die genannten Nachteile eines Listen Servers entfallen.

Die Konfiguration von Dedicated Servern lässt sich fernsteuern. Sie kann so auch mehreren Administratoren verwaltet
werden, selbst wenn diese nicht am Spielgeschehen teilnehmen. Auch können mehrere Instanzen auf einem Server betrieben
werden.

Zudem lassen sich sowohl die Konfigurationen als auch die verfügbaren Maps und Modifikationen sowie letztlich die
kompletten Server selbst mit entsprechenden Werkzeugen verfielfältigen und sogar dynamisch installieren und starten.
Das ist insbesondere für größere [Turniere](/wiki/turniere) nützlich, aber auch für die effizientere Nutzung von
verfügbaren Serverressourcen durch wechselnden bzw. temporären Betrieb verschiedener Dedicated Server.

Voraussetzung ist allerdings, dass für das jeweilige Spiel überhaupt Dedicated Server angeboten werden. Während dies
um die Hochphase von LAN-Partys um die Jahrtausendwende und folgend sehr gängig war (insbesondere bei Titeln der
Hersteller id Software und Valve), gibt es inzwischen viele Spiele, die auf vom Hersteller betriebene Server im Internet
angewiesen sind und die sich nicht lokal und unabhängig im LAN hosten lassen.
