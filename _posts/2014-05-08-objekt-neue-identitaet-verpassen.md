---
layout: post
title: "Objekt neue Identität verpassen"
category: posts
---
Ich habe mir letztens die Innerreien von Java genauer anguckt und etwas damit rumgespielt ;-). Konkret habe ich mir angeguckt, wie in Java Objekte und Klassen(definitionen) im Speicher gehalten werden.
In diesem Blog Post will ich mal eben zeigen, wie man in Java einer Instanz eine ganz andere Klasse zuweisen kann.
Fangen wir einfach ein. Zuerst werden zwei unabhängige Klasse benötigt. Zum Beispiel KlasseA und KlasseB. Beide Klassen haben nichts miteinander zu tun, besitzen aber die selbe Struktur (wobei dies egal ist).

{% highlight bash %}
public class ClassA {
    protected short s = 20;
}
{% endhighlight %}

{% highlight bash %}
public class ClassB {
    protected short s = 40;
}
{% endhighlight %}

Werden zwei Instanz erstellt, befinden diese sich natürlich im Speicher. Im Falle auf einer 64-bit Machine mit der JVM Option -XX:+UseCompressedOops (was bei vielen der Standard sein sollte) liegen beide Objekte in folgender Form im Speicher: 

```
8 byte [mark]
4 byte [klass pointer]
x byte [fields]
```

Für unseren Fall sind die 4 Byte vom Klassenpointer interessant. Dieser zeigt auf die Klassendefinition, in der die eigentliche Klasse beschrieben ist. Im Falle von einer Instanz vom Typ ClassA würde diesen 4 Byte auf die Speicheradresse zeigen, in der die Klasse ClassA beschrieben ist. Dort würde sowas stehen wie, Sichtbarkeit der Klasse, Superklassen usw.
Schaft man es nun, diese 4 Bytes im Speicher durch andere (valide) 4 Bytes auszutauschen, bekommt eine Instanz in Java eine ganz neue Identität verpasst. In diesem konkreten Beispiel würde eine Instanz von ClassA zu einem Typ von ClassB werden.

Wie kommt man nun an den Speicher und wie kann dieser geändert werden?
Dazu behelfen wir uns der Klasse sun.misc.Unsafe. Allerdings muss man sich beim Beschaffen einer solchen Unsafe-Instanz mittels Reflections behelfen.

{% highlight java %}
public static Unsafe getUnsafe() {
  try {
    Field f = Unsafe.class.getDeclaredField("theUnsafe");
    f.setAccessible(true);
    return (Unsafe)f.get(null);
  } catch (Exception e) { 
		throw new RuntimeException(e);
  }
}
{% endhighlight %}

Mit folgendem Code kann nun die Adresse einer Instanz ermittelt werden. Dazu wird ein Hilfs-Array erstellt und dort eine Instanz reingelegt. In diesem Fall eine Instanz vom Typ ClassA und ClassB.

{% highlight java %}
Object array[] = new Object[1];
array[0] = instance;
long baseOffset = unsafe.arrayBaseOffset(Object[].class);
long addressOfObject = unsafe.getLong(array, baseOffset);
{% endhighlight %}

Besitzt man nun beide Adressen von beiden kann nun einfach bei der einen Instanz die Adresse vom Klassen-Pointer ausgelesen werden und bei der anderen Instanz hineingeschrieben werden. Dafür nutzen wir die beiden Methoden getInt(Long) und putInt(Long, Integer) von der Klasse sun.misc.Unsafe.

{% highlight java %}
unsafe.putInt(
    addressOfClassA + 8, 
    unsafe.getInt(addressOfClassB + 8));
{% endhighlight %}

Nun ist unsere Instanz, erstellt mit new ClassA() ein Typ von ClassB.

{% highlight java %}
System.out.println(((ClassB) (Object) instanceOfClassA).s);
{% endhighlight %}