---
layout: post
title: "Primfaktorzerlegung in Clojure"
category: posts
---
Als kleiner Test für meinen ersten richtigen Blogeintrag poste ich einfach mal noch von damals meine Version der Primfaktorzerlegung in Clojure.

{% highlight clojure %}
(defn prime [x]
   (loop [counter 2
          number x
          result '()]
     (if (= 0 (mod number counter))
       (recur counter (/ number counter) (conj result counter))
       (if (= 1 number)
         result
         (recur (inc counter) number result))))) 
{% endhighlight %}