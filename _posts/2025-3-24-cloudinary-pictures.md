---
layout: post
title: Bilder extern hosten mit Cloudinary
categories: [IT, Blogging]
---
## Warum GitHub Pages nicht zum Bilder hosten gedacht ist
GitHub ist ein hervorragendes Werkzeug um Code zu verwalten, aber wenn es um Bilder geht nicht die erste Wahl. In meinem Blog möchte ich aber das eine oder andere Bild für euch mit anbieten (der Ästhetik wegen und so ;) ) und da stellt sich die Frage wie man das am besten anstellt.

Standardmäßig kann man natürlich ohne weiteres Bilder mit Jekyll direkt einbinden indem man ein Bild aus dem Assets Ordner platziert und das dann entsprechend im Blogpost referenziert:

```markdown
![My helpful screenshot](/assets/screenshot.jpg)
```

Das funktioniert hervorragend für kleine Bilder und wenn keine automatische Skalierung der angezeigten Bilder gefordert ist die über das resizen hinausgeht.

Nachteil: Die Bilder belegen Speicher im Repository. GitHub Pages hat für seine Seiten aber eine Limitierung von 1 GB. Das klingt erstmal viel, wenn man aber hochauflösende Bilder ausspielen will kommt man da bei einem größeren Blog oder längeren Fotostrecken schnell an seine Grenzen.

Verschärft wird das noch durch responsives Design bzw. die notwendige Skalierung. Ein Bild auf einem Handybildschirm braucht natürlich bei weitem nicht dieselbe Auflösung wie auf einem 4k oder 8k Monitor. Im Sinne der Datensparsamkeit und damit die Webseite schnell bleibt möchte man daher nur die notwendige Größe basierend auf dem Viewport des Nutzers ausspielen. Damit das funktioniert, muss dasselbe Bild in verschiedenen Auflösungen vorliegen, damit dann dynamisch das richtige Bild angezeigt werden kann. Das bedeutet zusätzliche (manuelle) Arbeit für die Erstellung dieser Bilder durch den Blogbetreiber und belastet zusätzlich das Github Repository.

## Die Lösung: Cloudhosting und CDN / Image CDN
Schick wäre es doch daher, wenn die Bilder nur einmalig abgelegt werden müssen und dann beim Seitenaufruf automatisch resized und direkt nur in der Größe geladen werden die für den Leser relevant ist. Das drückt zwar etwas auf die Ladezeit der Seite weil ein externer Service aufgerufen werden muss, spart uns aber die lokale Verwaltung der Files im GitHub Repository und der Service kann dann ja auch direkt das Resizing übernehmen.

Die einfachste Form wäre die Einbindung einer externen Bildquelle via image Tag.

```html
<img src="hhttps://res.cloudinary.com/dc0ncqsdx/image/upload/v1742813471/404_fwlf27.jpg" alt="Per Imag Tag eingebunden" width="32" height="32">
```
Ergebnis - per Image Tage von extern geladen:
<img src="https://res.cloudinary.com/dc0ncqsdx/image/upload/v1742813471/404_fwlf27.jpg" alt="Per Image Tag eingebunden" width="100" height="100">

Die Quelle kann ein beliebige Webquelle sein. Neben Cloudspeichern wie Google Drive, Dropbox oder Amazon S3 kommen dafür auch andere Github Repos in Frage. Das Resizing übernehmen diese aber noch nicht für uns, das ist also nur die halbe Miete.

Für Datenintensive Anwendungen bieten sich generell CDN (Content Delivery Network) an. Diese sind darauf ausgelegt massiv zu skalieren und große Datenmengen wie Bilder oder Videos effizient und schnell bereitzustellen ohne die eigentliche Website zu belasten. Insbesondere für Bilder gibt es dann noch spezialisierte Image CDN, die neben der reinen Bildbereitstellung auch noch Optionen zur Manipulation und Optimierung der Bilder anbieten, was automatisiert oder über URL direktiven (Parameter innerhalb der URL die Einfluss auf die Verarbeitung der Anfrage im CDN nehmen) erfolgen kann. Beispiele für Anbieter solcher Image CDNs sind Cloudflare, Imgix und Cloudinary.

Da ein kleiner frisch gestarteter Blog nicht zu kostenintensiv sein soll, bieten sich die kostenlosen Pläne der Anbieter an um herauszufinden ob die Lösung etwas für deine Webseite ist.

## Implementierung mit Cloudinary
Für meinen Blog habe ich mich für Cloudinary entschieden, da der kostenlose Free Plan relativ großzügig bemessen ist. Zum Zeitpunkt der Erstellung dieses Posts sind das 25 GB an Speicher, was für die meisten kleinen Blogs locker ausreichen sollte. Nähere Infos findest du hier: https://cloudinary.com/pricing

Der Login funktioniert praktischerweise auch direkt mit einem GitHub Account, da kann man sich die lästige Erstellung eines zusätzlichen Nutzerkontos direkt sparen.

### Variante Fetch mit eigener Datei
Wenn es rein um die Skalierung geht, lässt sich als Zwischenschritt die Fetch Funktion von Cloudinary benutzen. Diese kann mit einem lokal verfügbaren Bild aus dem GitHub Repository verwendet werden um  beim Seitenaufruf und Änderungen der Seitengröße das fragliche Bild aus dem Repo an Cloudinary zu übermitteln. Zurück kommt dann in der skalierten Form ein angepasstest Bild für die Anzeige.

Beispielcode:
```html
<img
  src="https://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_800,q_auto,f_auto/https://<your-domain>/assets/img.jpg"
  srcset="
    https://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_320,q_auto,f_auto/https://<your-domain>/assets/img.jpg 320w,
    https://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_640,q_auto,f_auto/https://<your-domain>/assets/img.jpg 640w
    https://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_960,q_auto,f_auto/https://<your-domain>/assets/img.jpg 960w
    https://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_1280,q_auto,f_auto/https://<your-domain>/assets/img.jpg 1280w
    https://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_1600,q_auto,f_auto/https://<your-domain>/assets/img.jpg 1600w
    "
  sizes="(min-width: 50rem) 50rem, 90vw"
  alt="beautiful!"
  width="480"
  height="320"
/>
```

Ergebnis - Bild aus dem Repo zur Laufzeit von Cloudinary skaliert:
<img
    src="https://res.cloudinary.com/{{ site.cloudinary_project }}/image/fetch/c_limit,w_800,q_auto,f_auto/{{site.enforce_ssl}}images/404.jpg"
    srcset="
        https://res.cloudinary.com/{{ site.cloudinary_project }}/image/fetch/c_limit,w_320,q_auto,f_auto/{{site.enforce_ssl}}images/404.jpg 320w,
        https://res.cloudinary.com/{{ site.cloudinary_project }}/image/fetch/c_limit,w_640,q_auto,f_auto/{{site.enforce_ssl}}images/404.jpg 640w,
        https://res.cloudinary.com/{{ site.cloudinary_project }}/image/fetch/c_limit,w_960,q_auto,f_auto/{{site.enforce_ssl}}images/404.jpg 960w,
        https://res.cloudinary.com/{{ site.cloudinary_project }}/image/fetch/c_limit,w_1280,q_auto,f_auto/{{site.enforce_ssl}}images/404.jpg 1280w,
        https://res.cloudinary.com/{{ site.cloudinary_project }}/image/fetch/c_limit,w_1600,q_auto,f_auto/{{site.enforce_ssl}}images/404.jpg 1600w
    "
    sizes="(min-width: 100px) 100px, 100px"
    alt="Loaded via fetch from cloudinary"
    loading="lazy"
/>

Ein Snippet für ein statisches HTML Template könnte dann folgendermaßen aussehen:
```liquid
{% raw %}{% if site.url contains "localhost" %}
<img src="{{ site.url }}{{ include.path }}" loading="{{ include.loading | default: "lazy" }}" />
{% else %}
<img
    src="https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/fetch/c_limit,w_800,q_auto,f_auto/{{ site.url }}{{ include.path }}"
    srcset="
        https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/fetch/c_limit,w_320,q_auto,f_auto/{{ site.url }}{{ include.path }} 320w,
        https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/fetch/c_limit,w_640,q_auto,f_auto/{{ site.url }}{{ include.path }} 640w,
        https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/fetch/c_limit,w_960,q_auto,f_auto/{{ site.url }}{{ include.path }} 960w,
        https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/fetch/c_limit,w_1280,q_auto,f_auto/{{ site.url }}{{ include.path }} 1280w,
        https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/fetch/c_limit,w_1600,q_auto,f_auto/{{ site.url }}{{ include.path }} 1600w
    "
    sizes="(min-width: 50rem) 50rem, 90vw"
    alt="{{ include.alt }}"
    loading="{{ include.loading | default: "lazy" }}"
/>
{% endif %}{% endraw %}
```

Damit verbleibt dann nur noch eine Version des Bildes bei uns im Repository, das erspart uns dann schon mal das Speichern des Bildes in verschiedenen Größen und skaliert auch jetzt schon sehr schön und zügig.

### Der externe Weg via Cloudinary Digital Asset Management
#### Das Auslagern der Bilder
Da unser Ziel war die Bilder komplett auszulagern, gehen wir nun noch einen Schritt weiter und werden bei Cloudinary verwaltete Bilder direkt skaliert anzeigen.

Dazu laden wir zunächst ein Bild bei Cloudinary hoch (an dem wir selbstverständlich die Bildrechte besitzen ;) ).

Mit der Funktion "Copy Link" lässt sich ein Link erstellen, mit dem das Bild öffentlich im Web abrufbar ist.

<!---Dieses Bild wurde direkt aus dem GitHub Repository geladen-->
![Copy Link in Cloudinary](/images/cloudinary_copy_link.jpg)

Beispiellink:
```html
https://res.cloudinary.com/dc0ncqsdx/image/upload/v1742813471/404_fwlf27.jpg
```

Der Link hat zwei wesentliche Informationen für uns:  
* Die Projekt ID von Cloudinary für unseren User. Diese wird bei allen Bildern die wir hochladen identisch sein.
* Den Pfad und Namen des Bildes. Der Dateiname hat sich mit dem Upload dezent verändert, das tut der Nutzbarkeit aber keinen Abbruch.

#### Anzeige in der eigenen Website
Als nächstes wollen wir das Bild auf unserer Webseite anzeigen.

Beispiel Code in Anlehnung an die Cloudinary Doku:
```html
<img
  sizes="(min-width: 50em) 50em, 100vw"
  srcset="https://res.cloudinary.com/demo/image/upload/f_auto/q_auto/c_scale,w_256/docs/house.jpg 256w,
          https://res.cloudinary.com/demo/image/upload/f_auto/q_auto/c_scale,w_512/docs/house.jpg 512w,
          https://res.cloudinary.com/demo/image/upload/f_auto/q_auto/c_scale,w_768/docs/house.jpg 768w,
          https://res.cloudinary.com/demo/image/upload/f_auto/q_auto/c_scale,w_1024/docs/house.jpg 1024w,
          https://res.cloudinary.com/demo/image/upload/f_auto/q_auto/c_scale,w_1280/docs/house.jpg 1280w"
  src="https://res.cloudinary.com/demo/image/upload/f_auto/q_auto/c_scale,w_512/docs/house.jpg"
  alt="Responsive house"
/>
```

Ergebnis - Direkt von Cloudinary skaliert geladen:
<!---Dieses Bild wurde direkt von Cloudinary skaliert geladen -->
  <img
  sizes="(min-width: 50rem) 50rem, 90vw"
  src="https://res.cloudinary.com/dc0ncqsdx/image/upload/f_auto/q_auto/c_scale,w_512/404_fwlf27.jpg"
  srcset="https://res.cloudinary.com/dc0ncqsdx/image/upload/f_auto/q_auto/c_scale,w_256/404_fwlf27.jpg 100w,
          https://res.cloudinary.com/dc0ncqsdx/image/upload/f_auto/q_auto/c_scale,w_512/404_fwlf27.jpg 200w"
  alt="Direkt von Cloudinary skaliert geladen" />

#### Template für bessere Wiederverwendbarkeit - statische Sizes
Diesen Code kann man jetzt direkt auf jeder Seite verwenden und sich Bilder in der gewünschten Größe von Cloudinary zur Anzeige abholen. Damit man diesen doch etwas länglichen Code nicht jedes mal schreiben muss was die markdown Seite ganz schön aufbläht und der Wartbarkeit abträglich ist, lagern wir den Code nun in ein separates File aus und holen uns den Code zum Generierzeitpunkt von Jekyll (nicht zum Ladezeitpunkt der Seite) mittels Liquid Include unter Angabe von zusätzlichen Parametern wie dem Bildnamen und die alt Text. Parameter die wir standardmäßig vorbelegen können, wie zum Beispiel die Cloudinary Projekt ID, lassen sich auch direkt aus der config.yml vorbelegen und müssen dann nicht jedes mal wieder mitgegeben werden.

Wenn deine Webseite mit Standardgrößen arbeitet, tut es eine parametrisierte Variante des obenstehenden Codes, das könnte dann ungefähr so aussehen: _includes/cloudinary_static.html

```html
<img
  sizes="(min-width: 50em) 50em, 100vw"
  srcset="https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_256/{{ include.picture_name }} 256w,
          https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_512/{{ include.picture_name }} 512w,
          https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_768/{{ include.picture_name }} 768w,
          https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_1024/{{ include.picture_name }} 1024w,
          https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_1280/{{ include.picture_name }} 1280w"
  src="https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_1280/{{ include.picture_name }}"
  alt="{{ include.alternative_text }}"
/>
```
Der zugehörige include im Post sieht dann folgendermaßen aus:
```liquid
{% raw %}
{% include cloudinary_static.html picture_name="404_fwlf27.jpg" alternative_text="Static include sizes" %}
{% endraw %}
```
... und führt zu folgendem Ergebnis:
{% include cloudinary_static.html picture_name="404_fwlf27.jpg" alternative_text="Static include sizes" %}

#### Template für bessere Wiederverwendbarkeit - parametrisierte Sizes mit Default
Da Bilder nicht immer exakt dieselbe Größe haben werden und sich daher nicht unbedingt gleich gut skalieren lassen, bietet es sich gegebenenfalls an die Skaliersizes nicht fix anzugeben, sondern ebenfalls als Parameter zu übergeben.

Dazu übergeben wir die Sizes als Liste und iterieren mittels Liquid im Template über die Einträge um den String für den Include (insbesondere das srcset) zusammenzubauen.

Der Code dafür kann dann beispielsweise so aussehen:
```liquid
{% raw %}{% assign default_sizes = site.cloudinary_scaling_sizes %}
{% assign include_sizes = include.sizes | split: ',' %}
{% assign final_sizes = include_sizes | default: default_sizes %}
{% assign srcset_string = "" %}

<img sizes="(min-width: 50rem) 50rem, 100vw" srcset="{% for size in final_sizes %}
        {% assign srcset_string = srcset_string | append: "https://res.cloudinary.com/" | append: site.cloudinary_project | append: "/image/upload/f_auto/q_auto/c_scale,w_" | append: size | append: "/" | append: include.picture_name | append: " " | append: size | append: "w" %}
        {% unless forloop.last %}{% assign srcset_string = srcset_string | append: ", " %}{% endunless %}
    {% endfor %}{{ srcset_string }}" src="https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_1280/{{ include.picture_name }}"
    alt="{{ include.alternative_text }}"/>{% endraw %}
```
Der zugehörige Include im Post gibt dann wieder die üblichen Parameter mit, aber zusätzlich die Sizes:
```liquid
{% raw %}{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with explicit sizes" sizes="100,200" %}{% endraw %}
```
Ergebnis - Explizite Size Angabe im Include (Das Bild wird etwas pixelig, weil die angegebenen sizes nicht optimal sind. Aber hey, immerhin sieht man, dass es funktioniert ;))
{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with explicit sizes" sizes="100,200" %}
Da sich doch oft Standardgrößen verwenden lassen, kann man den include optional auch ohne explizite size Angabe durchführen. Den Default geben wir dann im config.yml an. Damit sind wir dann einerseits flexibel wenn wir Sondergrößen benötigen, aber andererseits auch prägnant kurz in unserem Include wo immer ein Include mit den Standardgrößen möglich ist.

Der zugehörige Include sieht dann so aus:
```liquid
{% raw %}{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with default sizes" %}{% endraw %}
```
Und das Ergebnis so:
{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with default sizes" %}

Die angegeben Sizes haben nun zunächst einmal nur Auswirkungen auf die Skalierung des Bildes, nicht aber auf die Anzeigegröße. Werden hier noch zusätzliche Anpassungen benötigt muss man an das sizes Attribut ran, das ist aber eine Aufgabe für einen anderen Tag ;).

## Die fertige Lösung
Die Lösung die ich in meinem Blog verwende schaut nun in der Endausbaustufe folgendermaßen aus:

_config.yml:
```yml
cloudinary_project: "dc0ncqsdx" # Cloudinary project for remote image includes
cloudinary_scaling_sizes: [320,640,960,1280,1600] # Default sizes for scaling images
cloudinary_sizes_attribute: "(min-width: 50rem) 50rem, 100vw" # Default sizes attribute for image rendering
```

_includes/cloudinary_configurable.html:
```
{% raw %}{% assign default_scaling_sizes = site.cloudinary_scaling_sizes %}
{% assign include_scaling_sizes = include.sizes | split: ',' %}
{% assign final_scaling_sizes = include_scaling_sizes | default: default_scaling_sizes %}
{% assign srcset_string = "" %}
{% assign default_sizes_attribute = site.cloudinary_sizes_attribute %}
{% assign include_sizes_attribute = include.sizes_attribute %}
{% assign final_sizes_attribute = include_sizes_attribute | default: default_sizes_attribute %}

<img sizes="{{ final_sizes_attribute }}" srcset="{% for size in final_scaling_sizes %}
        {% assign srcset_string = srcset_string | append: "https://res.cloudinary.com/" | append: site.cloudinary_project | append: "/image/upload/f_auto/q_auto/c_scale,w_" | append: size | append: "/" | append: include.picture_name | append: " " | append: size | append: "w" %}
        {% unless forloop.last %}{% assign srcset_string = srcset_string | append: ", " %}{% endunless %}
    {% endfor %}{{ srcset_string }}" src="https://res.cloudinary.com/{{ site.cloudinary_project }}/image/upload/f_auto/q_auto/c_scale,w_1280/{{ include.picture_name }}"
    alt="{{ include.alternative_text }}"/>{% endraw %}
```
_post/name_des_tollen_neuen_posts.md
```liquid
Default Sizes:
{% raw %}{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with default sizes" %}{% endraw %}

Manuelle Sizes:
{% raw %}{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with explicit sizes" sizes="100,200" %}{% endraw %}

Explizite Size Attribut Angabe:
{% raw %}{% include cloudinary_configurable.html picture_name="404_fwlf27.jpg" alternative_text="Configurable include sizes with explicit sizes and sizes attribute" sizes="100,200" cloudinary_sizes_attribute="(min-width: 50rem) 50rem, 100vw"%}{% endraw %}
```

Für mich funktioniert diese Variante ganz hervorragend. Sie ist natürlich nicht für jedes Bild auf der Webseite der richtige Weg, aber für die üblichen in Posts vorkommenden Anwendungsfälle erspart es mir einiges an Tipparbeit und hält das Repository schön klein.

Was denkst du dazu? Über Feedback und Verbesserungsvorschläge freue ich mich und auch über eine kurze Nachricht wenn der Post für dich hilfreich war.

Hotstone out.

## Weitere Ressourcen
* Im [Quellcode dieser Seite](https://github.com/john-hotstone/john-hotstone.github.io/blob/master/_posts/2025-3-24-cloudinary-pictures.md) findest du übrigens Beispiele für ein paar der besprochenen Varianten, also schau gerne dort rein wenn dich die tatsächliche Implementierung interessiert.
* Ein Post, der beschreibt wie die Fetch Funktion verwendet werden kann um Bilder aus dem Repository mit Cloudinary zu skalieren ist [hier](https://tiberriver256.github.io/jekyll/web%20development/jekyll-cloudinary-github-compatible-snippet/) zu finden. Von dort stammt auch das wiederverwendbare HTML Template Snippet von oben.
* Ein [Jekyll Plugin](https://github.com/nhoizey/jekyll-cloudinary) das einen Liquid Tag anbietet um die Fetch Funktion noch bequemer aufrufen zu können.
* Die [Dokumentation von Cloudinary](https://cloudinary.com/documentation/responsive_html) beschreibt ziemlich genau was ich bei mir umgesetzt habe mit Abruf der Bilder aus dem Cloudinary Asset Management
