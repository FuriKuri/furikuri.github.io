---
layout: post
title: "Hello World Webanwenung in Clojure erstellen"
category: posts
---
In diesem Post schreibe ich kurz nieder, wie innerhalb von wenigen Minuten eine lauffähige Webanwendung in Clojure geschrieben werden kann.
Zuerst sollte sichergestellt sein, dass Leinigen installiert ist.  Unter nem Mac mit Brew kann dies über folgenden Befehl installiert werden:
{% highlight bash %}
$ brew install leiningen
{% endhighlight %}
Für andere Plattformen werden aber ebenfalls Installationsskripte zur Verfügung gestellt. [Link zum Github-Projekt](https://github.com/technomancy/leiningen)
Ist Leiningen installiert, kann auch nun schon direkt ein Web-Projekt erstellt werden:
{% highlight bash %}
$ lein new compojure-app hello-world
{% endhighlight %}
Wenn man sich nun in das Projekt bewegt, kann schon direkt ein Server gestartet werden, womit die Anwendung dann unter [http://localhost:3000](http://localhost:3000) erreichbar ist.
{% highlight bash %}
$ cd hello-world
$ lein ring server
{% endhighlight %}
Viel Spass beim rumprobieren!