---
layout: post
title: "Simples Elixir Projekt erstellen"
category: posts
---
Ich habe mir die letzten die Programmiersprache Elixir näher angeguckt. Wenn man sich etwas mehr damit befasst, findet man ein paar sehr interessante Dinge. In diesem Post will ich erstmal nur die ersten Schritte beim Erstellen eines Projektes runterschreiben.

Voraussetzung ist natürlich, dass Elixir auf dem Rechner installiert ist. Aktuell ist die Version 0.13. Diese kann einfach mit Homebrew installiert werden.

{% highlight bash %}
$ brew install elixir
{% endhighlight %}

Die Elixir Version 0.13 benötigt die relativ neue Erlang Version 17.0, welche, wenn Homebrew benutzt wird, zur Zeit gesondert installiert werden muss. So ist aktuell im Homebrew Repository nur die Version R16B03. Die 17.0 Version kann folgendermaßen installiert werden:

{% highlight bash %}
$ brew install erlang --devel
{% endhighlight %}

Ist Elixir installiert, kann mit Hilfe von `mix` ein Projekt generiert werden. `mix` ist von Build-Tool, welches von Elixir mitgebracht wird. In diesem Beispiel wird ein Projekt names `hello` erstellt.

{% highlight bash %}
$ mix new hello
{% endhighlight %}

Anschließend kann in das neue Verzeichnis gewechselt werden. In diesem kann direkt mal der Befehl `mix test` ausgeführt werden. Dieser führt die Testfälle aus, welche beim erstellen des Projektes automatisch erstellt worden. 

{% highlight bash %}
$ cd hello
$ mix test
{% endhighlight %}

Prinzipiell steht somit das Projekt. Wir machen hier zusätzlich aber noch einen Schritt und zwar wollen wir unser "Hello"-Projekt noch von unserer Konsole aus starten. Dafür erstellen wir ein neues Modul in `lib/cli.ex`, welches einfach nur "Hello World" ausgibt.

{% highlight elixir %}
defmodule Hello.CLI do
	def main(args) do
    	IO.puts "Hello World"
  	end
end
{% endhighlight %}

Damit `mix` auch das Modul kennt, welches beim Start verwendet werden soll, muss diese noch in der Projekt-Konfiguraion `mix.exs` angegeben werden. Dazu muss einfach `escript_main_module: Hello.CLI` in der `project`-Function hinzugefügt werden. Die Datei `mix.exs` sieht dann folgendermaßen aus:

{% highlight elixir %}
defmodule Hello.Mixfile do
  use Mix.Project

  def project do
    [app: :hello,
     version: "0.0.1",
     elixir: "~> 0.13.0",
     escript_main_module: Hello.CLI,
     deps: deps]
  end

  def application do
    [ applications: [],
      mod: { Hello, [] } ]
  end

  defp deps do
    []
  end
end
{% endhighlight %}

Ist dies geschehen kann mit `mix escriptize` eine ausführbares Skript erstellt werden, welches dann auch direkt ausgeführt werden kann. Diese müsste nun "Hello World" ausgeben :)

{% highlight bash %}
$ mix escriptize
$ ./hello
{% endhighlight %}
