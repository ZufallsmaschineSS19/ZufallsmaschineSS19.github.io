# Untersuchung von Pseudo-Zufallszahlen mithilfe von Neuronalen Netzwerken

## Einleitung
Wie zuvor bereits erklärt wurde haben Zufallszahlen viele Anwendungsbereiche, besonders in der Cryptographie, beim Glücksspiel 
oder bei Simulationen. Die Überprüfung der Güte solcher Zufallszahlen ist deshalb eine wichtige aber auch schwierige Aufgabe. 
Hierzu gibt es bereits viele Tests, welche allerdings für sich allein selten eine Aussage über die Güte der Zufallszahlen gibt.
So kann eine Zahlenfolge einen Test bestehen, jedoch in allen anderen Durchfallen oder bei Untersuchung von Teilstücken einer
Folge von Zufallszahlen einige bestehen und andere nicht.Hier liegt vorallem das Problem vor, dass immer nur eine Endliche 
Folge vorliegt, wirklich Zufall allerdings nur bei einer unendlich langen Folge untersucht werden könnte.

Eine völlig andere Idee als bei herkömmlichen Tests, in denen jeweils Gewisse Kriterien überprüft werden, ist die Nutzung von 
Maschinellem Lernen (machine-learning). Dabei sind besonders Neuronale Netzwerke weit verbreitet und erbringen erstaunliche 
Ergebnisse in vielen Bereichen. Die Idee ist also, ein Neuronales Netzwerk zu nutzen um Pseudo ('pseudo random numbers'-PRN),- 
aber auch Echte ('true random numbers'-TRN) Zufallszahlen zu überprüfen und gegebenfalls versteckte Korrelationen zwischen den Daten aufzudecken. 
So soll deren Güte aufgrund der Vorhersagbarkeit der Zahlenfolgen (welche im Falle von binären Bitfolgen natürlich 
eigentlich bei 50% liegen sollte) überprüft werden.



und dort besonders NeuronalenHierbei ergibt sich nun die Idee
