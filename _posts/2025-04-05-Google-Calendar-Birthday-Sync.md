---
layout: post
title: Google Calendar Geburtstage syncen (auch in Deutschland)
categories: [IT]
---
Hast du dich auch kürzlich mal gewundert, warum die Kalenderapp auf dem Handy plötzlich so leer erscheint oder hast du Tante Ernas Geburtstag vergessen, weil dich deine künstliche Hosentaschenintelligenz nicht rechtzeitig daran erinnert hat? Wenn du auch so wie ich für Geburtstagserinnerungen bisher die Daten in deine Kontakte auf dem Handy eingetragen hast, hab ich hier des Rätsels Lösung für dich und die ist irgendwas zwischen unterhaltsam und einfach nur ärgerlich.

Wenn man die Berichterstattung dazu nicht zufällig verfolgt hat, hat sich der Kalender schnell mal heimlich still und leise von einem Tag auf den anderen geleert und man wundert sich was mit den ganzen Terminen passiert ist, die jahrelang und über mehrere Handys ohne Probleme angezeigt wurden jetzt aner ganz offensichtlich fehlen.

Um Regularien für die Verknüpfung von Daten im Deutschland zu entsprechen, sah sich Google veranlasst die Verknüpfung zwischen den Daten verschiedener Apps wie zum Beispiel der Kontakte App und Kalender App aufzugeben und diese nicht mehr miteinander zu synchronisieren.

Google selbst verweist dabei auf eine "Vereinbarung mit einer deutschen Regulierungsbehörde" (siehe [hier](https://support.google.com/calendar/answer/13748346?hl=de&co=GENIE.Platform%3DAndroid))

Vor einigen Monaten ist das schonmal passiert, da konnte man den Sync aber noch manuell reaktivieren und so seine Kontaktgeburtstage retten. Damit ist jetzt Schluss, Google hat für Deutschland den Stecker für dieses - aus meiner Sicht doch Recht praktische Feature - gezogen und Daten aus den Kontakten können nicht mehr im Kalender angezeigt werden. Ade Geburtstagsreminder.

Als Alternative soll man nun Geburtstage direkt im Kalender als Termin pflegen, dafür gibt es auch einen eigenen Eventtyp.

Das hilft natürlich jetzt nicht dabei alle meine 587 Kontakte händisch zu migrieren und eigentlich möchte ich auch weiterhin die Geburtstage lieber direkt an meinen Kontaken pflegen und nicht als Termin. Postalische und digitale Adressen und sonstige personenbezogene Daten sind da ja auch hinterlegt, warum also trennen?

Zum Glück gibt es findige Leute auf der Welt, die eine (für IT Laien zugegebenermaßen etwas sperrige) Lösung für das Problem erarbeitet haben.

Eine gute Erläuterung findet sich [hier](https://stadt-bremerhaven.de/geburtstage-im-google-kalender-werden-nicht-angezeigt-so-klappt-es-wieder/)

Mithilfe des dort angebotenen Scripts kann man dann zumindest eine einmalige Migration von den Kontakte in den Kalender durchführen. Für Traditionalisten wie mich, die sich nicht umgewöhnen wollen, kann man das dann auch noch regelmäßig automatisiert auf Googleeigener Infrastruktur laufen lassen und so den Sync doch noch retten.

Disclaimer: Das Script schaut erstmal harmlos aus und viel sollte da nicht passieren können, nichtsdestotrotz erteilt man dem Script natürlich weitreichende Berechtigungen für Kalender und Kontakte, das sollte man zumindest im Hinterkopf behalten. Auch kann es sein, dass sich zukünftig die APIs bei Google ändern und das Script nicht mehr funktioniert. Für mich sind das aber Probleme für mein Zukunfts-Ich und einstweilen bin ich einfach froh, dass Tante Erna wieder im Kalender erscheint.

Ich hoffe ein paar anderen leidgeprüften hiermit weitergeholfen zu haben. Wir Google Opfer müssen zusammenhalten.

Hotstone out.
