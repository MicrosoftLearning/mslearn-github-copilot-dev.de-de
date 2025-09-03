---
title: Übungsanweisungen
permalink: index.html
layout: home
---

# GitHub Copilot-Übungen

Die folgenden Schnellstartübungen bieten Ihnen eine praktische Lernerfahrung, durch die Sie die Funktionen von GitHub Copilot kennenlernen. Jede Übung umfasst eine Reihe von Aufgaben, die Sie in Ihrer Labumgebung ausführen können.

## Schnellstartübungen
<hr>

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}

{% for activity in labs  %}

### [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }})
{{ activity.lab.description }}
<hr>
{% endfor %}
