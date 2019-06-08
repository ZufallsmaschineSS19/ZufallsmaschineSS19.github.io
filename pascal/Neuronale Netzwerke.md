# Untersuchung von Pseudo-Zufallszahlen mithilfe von Neuronalen Netzwerken

## Einleitung
Wie zuvor bereits erklärt wurde, haben Zufallszahlen viele Anwendungsbereiche, besonders in der Cryptographie, beim Glücksspiel 
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


## Was ist machine learning eigentlich?
Im machine learning gibt es verschiedene Disziplinen. Hier soll sich mit dem 'supervised learning' Beispielsweise mit Neuronalen Netzwerken, beschäftigt werden. Beim 'supervised learning' wird ein Problem durch einen Input und einen dazugehörigen markierten Output beschrieben. Als Beispiel kann hier eine Folge von Zufallszahlen genommen werden. Der Input könnten die ersten 5 Zahlen der Folge sein, der zugehörige Output die 6. Zahl der Folge. Diese Paare von Inputs und Outputs werden auch Trainings-Set oder Trainings-Daten genannt. Ein anderes, weitaus bekannteres Beispiel, wäre die Klassifikation eines Bildes (also die Pixel als Inputs) in Katze oder nicht Katze (Output). 
Das Neuronale Netzwerk bzw. die Netzwerk-Funktion, die von den Inputs zu den Outputs abbildet, wird dann mithilfe des 'Backpropagation'-Algorythmus optimiert, um die gewählten Trainings-Daten möglichst gut zu Beschreiben. 

Dies ist nur eine sehr kurze und oberflächliche Beschreibung, 

## Idee und erste Tests
Bei den ersten Untersuchungen wurde sich besonders an dem Paper 'Learning from Pseudo-Randomness with an
Artificial Neural Network– Does God Play Pseudo-Dice?' von Fenglei Fan und Ge Wang orientiert.

Wie fügt man hier Quellen ein???!!!

In dieser Arbeit wurden die Nachkommastellen der Zahl \pi auf ihre Zufälligkeit untersucht. 

