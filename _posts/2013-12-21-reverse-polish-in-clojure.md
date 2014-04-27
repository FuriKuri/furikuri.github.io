---
layout: post
title: "Reverse Polish in Clojure"
category: posts
---
Der nächste Codezetzen, den ich präsentieren möchte, ist eine Implementierung der RPN. Umgesetzt habe ich dies, in dem eine unendliche Sequence erzeugt wird, welche die einzelenen Schritte beinhaltet, in welche die RPN aufgelöst wird.
{% highlight clojure %}
 (defn calc-next-step [input]
   (if (= 1 (count input)) input
     (loop [[x y] input
            [op & rest-input] (nthnext input 2)
            output ''()]
       (if (number? op)
         (recur [y op] rest-input (concat output (list x)))
         (concat output `(~(op x y)) rest-input )))))
  
 (defn rpn-seq [input]
   (iterate (fn [n] (calc-next-step n)) input))
{% endhighlight %}
Der Output kann folgendermaßen aussehen. Ich habe aus Lesbarkeitsgründen die Ausgabe formatiert, und die Clojure-Operatoren durch Zeichen ersetzt, die man dann auch lesen kann ;-). Ansonsten würde der Multiplikator folgendermaßen aussehen:
{% highlight bash %}
#<core$_STAR_ clojure.core$_STAR_@3e2f1b1a>
{% endhighlight %}
Hier die formatierte Ausgabe
{% highlight clojure %}
(take 5 (rpn-seq [12 2 3 + 2 * 5 / -]))
 ((12 2 3 + 2 * 5 / -)
 (12 5 2 * 5 / -)
 (12 10 5 / -)
 (12 2 -)
 (10))
{% endhighlight %}
