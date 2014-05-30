---
layout: post
title: "Eigener Blog mit Github"
category: posts
---
Dieser Blog wird komplett kostenlos über Github verwaltet und gehostet. Vielleicht ist das auch für andere interessant. Deswegen folgt hier eine knappe kompakte Anleitung, wie mit Jekyll und GitHub innerhalb von ein paar Minuten ein eigener Blog online gestellt werden kann.

Am einfachsten ist es ein bestehendes Jekyll-Projekt auf GitHub zu forken. Auf <a href="http://jekyllthemes.org/">jekyllthemes.org/</a> finde sich ein paar Themes mit den Links zu den Projekten. Habt ihr ein Theme gefunden, welches euch gefällt, könnte ihr dieses runterladen oder einfacher über GitHub forken. Passt nun ein paar Files in euerm Repository an. Welche Files das sind, steht meistens in der Installationsanleitung des jeweiligen Themes. Oft sind das Dateien wie "_config.yml", "CNAME" und die Posts im Verzeichnis "_post".

Ist das geschafft könnt ihr eueren Blog erstmal Lokal laufen mit <code>jekyll serve</code>. Sieht das gut aus, was dort zu sehen ist, könnt ihr das auf GitHub pushen. Nennt ihr nun das Repository in folgenden Namen um <username-von-github>.github.io könnt ihr eueren Blog unter http://githubusername.github.io erreichen.
