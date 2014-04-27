---
layout: post
title: "Angeguckt: Spring Boot (Groovy)"
category: posts
tags: "Groovy"
---
Ich hab mir heute mal das Projekt Spring Boot etwas genauer angeschaut. Spring Boot zielt darauf hinaus, die Entwicklung mit Spring noch weiter zu vereinfachen. Informationen zu Spring Boot gibt es auf der Projekt Seite von [Spring](http://projects.spring.io/spring-boot/).
In diesem Post werde ich die Groovy-Variante mit Spring Boot vorstellen. Morgen (oder wann später) mache ich das für Java. Dann werde ich ggf. auch näher auf bestimmte Elemente eingehen.
Für die Groovy Variante muss erstmal Spring Boot CLI installiert werden. Mit brew sieht das folgendermaßen aus:

{% highlight bash %}
$ brew tap pivotal/tap
$ brew install springboot
{% endhighlight %}

Für andere Plattformen findet ihr die Informationen auf der [GitHub-Seite](https://github.com/spring-projects/spring-boot).
Nun wird ein Groovy-File names app.groovy erstellt mit folgendem Inhalt:

{% highlight groovy %}
@Controller
class ThisWillActuallyRun {

    @RequestMapping("/")
    @ResponseBody
    String home() {
        return "Hello World!"
    }
}
{% endhighlight %}

Wenn nun mit Hilfe des Spring Boot CLI das Skript ausgeführt, kann, in diesem Fall eine einfache Webanwendung, unter [http://localhost:8080](http://localhost:8080) aufgerufen werden.

{% highlight bash %}
$ spring run app.groovy 
{% endhighlight %}

