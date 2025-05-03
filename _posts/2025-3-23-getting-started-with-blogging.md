---
layout: post
title: Getting started with Blogging
categories: [IT, Blogging]
---
Hattest du jemals Lust einen Blog zu verfassen um die Welt an deinen Gedanken, Erfahrungen und Erlebnissen teilhaben zu lassen? Die Gründe mögen vielfältig sein, aber am Anfang stehen in jedem Fall einige Grundsatzüberlegungen und -entscheidungen, die man anstellen und fällen sollte. Dieser Artikel soll sich jetzt weniger um die inhaltliche Ausrichtung oder Sinnhaftigkeit eines solchen Vorhabens drehen (liest überhaupt noch jemand Blogs?), sondern sich mit der Technik auseinandersetzen. Das eine oder andere funktioniert dann natürlich auch für beliebige andere Webseiten und nicht nur für Blogs, aber ich bleibe mit meinen Ausführungen nach Möglichkeit bei dem, was ich hier selbst versuche und das ist nun mal das Bloggen ;).

## Wohin mit meinem Blog?
Einen Blog einzurichten ist heutzutage kein Hexenwerk mehr. Bevor man damit aber startet sollte man sich im Klaren darüber sein welchen Aufwand man monetär und zeitlich in den Blog investieren möchte und wie viel dafür dann auch für die Technik draufgehen darf. Am einen Ende der Skala gibt es fertige Blogplattformen, bei denen man nach einer Anmeldung schon losbloggen kann und damit in kürzester Zeit schon live ist. Viel Individualisierung und Sonderwünsche sind dann aber nicht drin.
Am anderen Ende des Spektrums stehen hochflexible Eigenbauten, vielleicht sogar mit eigener Serverinfrastruktur. Damit ist so gut wie alles machbar, aber es erfordert schon ein bisschen mehr Arbeit als die fertige Lösung.
 

Als IT affiner Bastler mit Progammierbackground stört es mich zum Beispiel wenig mir auch mal im Quellcode die Finger schmutzig zu machen oder mit einer Versionsverwaltung zu hantieren. Für das Blogging ist da nicht allzu viel nötig, aber wen das schon schreckt, der ist mit einer Blogging Plattform vielleicht doch besser bedient.

Hier mal ein Versuch das Spektrum grob zu Clustern:
* Blogging Plattform: Tooling und Hosting aus einer Hand. Anmelden und loslegen. (z.B. Wordpress.com, Blogger, Medium)
* Website-Builder: Nicht explizit für das Blogging, daher gibt es oft mehr Flexibilität durch Plugins und Konfigurierbarkeit (z.B. Wix, Squarespace, Weebly)
* Selbstgehosteter Blog: Hier hat man schon einige Freiheitsgrade, aber technisches Verständnis ist definitiv notwendig (z.B. WordPress.org, Ghost)
* DIY-Lösung: Hosting selbst organisieren (zwischen einem managed hosting mit One-click Installation und eigenem Server daheim im Schrank ist alles drin) und dann die Website eigenständig programmieren. Viel Flexibilität, ein nicht zu unterschätzender Initialaufwand, wenn man es richtig machen möchte. (z.B. Netlify, GitHub Pages, Vercel)

## Start small
Ein wesentlicher Faktor für mich, als ich mit dem Bloggen anfangen wollte, waren die Kosten. Wer wird meinen Blog denn überhaupt lesen und lohnt sich dafür ein vollständiges Webhosting mit großen Maschinen für den ganzen Traffic den ich zu erwarten habe? Wenn man frisch startet, ist es nicht unwahrscheinlich, dass man erst mal eine Phase des organischen Wachstums durchmacht. Vielleicht wird es auch nie für die Allgemeinheit interessant und es bleibt einfach immer ein kleines Freizeit- und Hobbyprojekt. Daher war für mich schnell klar: Start small. Geringer Ressourceneinsatz, geringe Kosten. Wenn es kostenlose Möglichkeiten gibt, die ein bisschen mehr Zeit erfordern: go for it.

Generell kamen nach einiger Recherche daher zwei Varianten für mich in Frage: Ein günstiges managed hosting mit einem einschlägigen CMS (Content Management System), vorzugsweise Wordpress (ist vermutlich nicht ohne Grund mit ~60% Markanteil einer der größten Player am Markt) oder eine DIY-Lösung mit einem Static Site Generator (das drückt die Kosten für das Hosting deutlich). Wordpress hat den Charme, dass es eine unbegrenzte Auswahl an direkt nutzbaren und oft kostenlosen Plugins, Add-Ons, Themes etc. gibt. Wenn du ein Problem hast, gibt es mit Sicherheit dort draußen eine Lösung dafür. Die Komplexität des ganzen kann einen dabei aber auch schnell erschlagen, das Tool ist halt doch für mehr konzipiert als nur für das Bloggen. Wenn später mal noch ein Chat, ein Forum ein Webshop oder ähnliches dazu kommen soll: Wordpress is the way to go. Für mein Vorhaben ist es aber zumindest zu Beginn ein funktionaler Overkill. Zudem sind die Kosten für Webhosting in den letzten Jahren doch deutlich gestiegen und für einen Wordpress Blog muss man doch immerhin ein paar Euronen in die Hand nehmen. (Wordpress.com bietet zwar kostenlose Blogs, aber nur als Subdomain oder man braucht einen kostenpflichtigen Tarif)

Aufgrund der Feature- und Kostenüberlegungen, und auch weil ich mal etwas Neues sehen und lernen wollte ("Joomla und Wordpress sind ja ganz nett, aber was gibt es sonst noch da draußen?") habe ich mich für Jekyll als Static Site Generator entschieden und ein kostenloses Hosting via GitHub Pages. Der Mitteleinsatz ist tatsächlich minimal bei dieser Variante, für den Start kostet das keinen einzigen Cent. Und wenn es später doch mehr sein soll, ist ein Blog der ohnehin als Quelltext vorliegt vermutlich auch nicht allzu kompliziert umzuziehen.

Ein paar Cent wollte ich dann aber doch investieren, um eine Custom Domain zu verwenden. github.io ist zwar ganz passabel aber ein bisschen Individualität war mir dieses Projekt dann doch wert ;). Empfehlen kann ich beispielsweise [netcup](https://www.netcup.com/de/domains/domain-kaufen), dort gibt es immer mal wieder Angebote für spottbillige de Domains.

## Was muss der Blog alles können?
Nachdem die Technikfrage für mich geklärt war, ging es an das minimale Feature Set, das der Blog benötigen würde, damit ich mich anschließend auf das Erzeugen der Inhalte konzentrieren kann. Hier meine grundsätzliche Checkliste, die ich mir vorgenommen habe (und die dann auch in dem einen oder anderen Blogeintrag noch verwurstet wird):
* Zweckmäßige aber ansprechende Optik
* Hosting unter einer Custom Domain
* Blogeinträge offline verfassen (um beispielsweise unterwegs ohne Internetverbindung noch Content vorbereiten zu können)
* Rechtliche notwendige Seiten und Informationen (Impressum, Datenschutzerklärung etc.)
* Drafts von Blogeinträgen testweise publizieren und lektorieren durch Dritte ermöglichen
* Testinstanz für Codeänderungen an der Website selbst (z.B. Einführung neuer Funktionalität, neues Layout etc.)
* DSGVO-konformes Cookie Handling (Warum überhaupt Cookies? Siehe nächster Punkt)
* Einbindung von Google Analytics (mich interessiert dann schon ob die Artikel auch gelesen werden ;))
* Kategoriensystem  für Blogposts (Um verschiedene Themen zu behandeln; das soll ja kein monothematischer Blog werden und etwas Struktur schadet nicht)

Nice to have:
* Kommentarfunktion für Blogposts (Genaugenommen braucht es das nicht, Kommunikation geht auch via Social Media, Mail etc. Schick wäre es aber schon die Kommentare direkt am Artikel zu haben)
* Reading Progress Bar (Ja, ich  neige zu langatmigen Ausführungen. Immerhin siehst du so jederzeit, wo das Elend endet ;))
* (Externe) Verwaltung von Bildern aus den Blogposts (GitHub ist vieles, aber keine Bildverwaltung :P)
* Automatische Ergänzung von konditionalen Inhalten beispielsweise basierend auf der Kategorie des Eintrags aber auch automatisches Flagging von Reflinks o.Ä.


## Let's-A Go
Nachdem nun klar ist, wo die Reise hingehen wird, widmen wir uns den einzelnen Herausforderungen, die das Abenteuer Blogging mit sich bringt. In den nächsten Blogeinträgen teile ich mit euch ein paar Lösungsansätze, die ich auf dieser Seite selbst umgesetzt habe. Wenn es dir zusagt, kannst du gerne das eine oder andere weiterverwenden, in jedem Fall freue ich mich aber über deine Gedanken und Feedback.

Und nun: Los gehts :).