---
layout: post
title: "Objekt neue Identität verpassen"
category: posts
---
Ich habe mir letztens die Innerreien von Java genauer anguckt und etwas damit rumgespielt ;-). Konkret habe ich mir angeguckt, wie in Java Objekte und Klassen(definitionen) im Speicher gehalten werden.
In diesem Blog Post will ich mal eben zeigen, wie man in Java einer Instanz eine ganz andere Klasse zuweisen kann.

Grundsätzlich geht es um die Klasse `sun.misc.Unsafe`. Mit Hilfe dieser Klasse kann auf den Speicher der JVM zugegriffen werden.