---
layout: post
title: Google Calendar Geburtstage syncen (auch in Deutschland)
categories: [IT]
---
Hat sich noch jemand gewundert warum der Kalender auf dem Handy plötzlich so leer erscheint oder hast du Tante Ernas Geburtstag vergessen weil dich deine künstliche Hosentaschenintelligenz nicht daran erinnert hat? Wenn du auch so wie ich für Geburtstage bisher deine Kontakte auf dem Handy verwendest hast, hab ich hier des Rätsels Lösung für dich und die ist irgendwas zwischen unterhaltsam und einfach nur ärgerlich.

Wenn man die Berichterstattung dazu nicht zufällig verfolgt hat ist das schnell mal heimlich still und leise von einem Tag auf den anderen passiert und man wundert sich was mit den ganzen Terminen passiert ist die jahrelang und über mehrere Handys ohne Probleme angezeigt wurden, jetzt aber nicht mehr.

Weil sich sich Regularien für die Verknüpfung von Daten im Deutschland offensichtlich geändert haben, sah sich Google veranlasst die Verknüpfung zwischen den Daten verschiedener Apps wie zum Beispiel der Kontakte und App und Kalender App aufzugeben und diese nicht mehr miteinander zu synchronisieren.

Google selbst verweist dabei auf eine "Vereinbarung mit einer deutschen Regulierungsbehörde" (siehe [hier](https://support.google.com/calendar/answer/13748346?hl=de&co=GENIE.Platform%3DAndroid))

Vor einigen Monaten ist das schonmal passiert, da konnte man den Sync aber noch manuell reaktivieren und so seine Kontaktgeburtstage retten. Damit ist jetzt Schluss, Google hat für Deutschland den Stecker für dieses - aus meiner Sicht doch Recht praktische Feature - gezogen.

Als Alternative soll man nun Geburtstage direkt im Kalender pflegen, dafür gibt es auch einen eigenen Eventtyp.

Das hilft natürlich jetzt nicht alle meine 587 Kontakte händisch zu migrieren und eigentlich möchte ich auch weiterhin die Geburtstage direkt an meinen Kontaken pflegen.

Zum Glück gibt es hier findige Leute, die eine (für IT Laien zugegebenermaßen etwas sperrige) Lösung für das Problem anbieten.

Eine gute Erläuterung findet sich [hier](https://stadt-bremerhaven.de/geburtstage-im-google-kalender-werden-nicht-angezeigt-so-klappt-es-wieder/)

Mithilfe des Scripts kann man dann zumindest eine einmalige Migration durchführen. Für Traditionalisten wie mich, die sich nicht ungewöhnen wollen, kann man das dann auch noch regelmäßig automatisiert auf Googleeigener Infrastruktur laufen lassen und so den Sync doch noch retten.

Disclaimer: Das script schaut erstmal harmlos aus und viel sollte da nicht passieren können, nichtsdestotrotz erteilt man dem Script natürlich weitreichende Berechtigungen für Kalender und Kontakte, das sollte man zumindest im Hinterkopf behalten. Auch kann es sein dass sich zukünftig die APIs bei Google ändern und das Script nicht mehr funktioniert. Fur mich sind das aber Probleme für mein Zukunfts-Ich und einstweilen bin ich einfach froh, dass Tante Erna wieder im Kalender erscheint.

Ich hoffe ein paar anderen leidgeprüften hiermit weitergeholfen zu haben. Wir Google Opfer müssen zusammenhalten.

Hotstone out.
