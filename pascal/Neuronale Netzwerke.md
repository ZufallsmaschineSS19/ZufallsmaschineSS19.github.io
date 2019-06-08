# Untersuchung von Pseudo-Zufallszahlen mithilfe von Neuronalen Netzwerken

## Einleitung
Wie zuvor bereits erklärt wurde, haben Zufallszahlen viele Anwendungsbereiche, besonders in der Cryptographie, beim Glücksspiel 
oder bei Simulationen. Die Überprüfung der Güte solcher Zufallszahlen ist deshalb eine wichtige aber auch schwierige Aufgabe. 
Hierzu gibt es bereits viele Tests, welche jeweils einzelne Eigenschaften von Zufallszahlen überprüfen, jedoch für sich allein selten eine Aussage über die Güte der Zufallszahlen geben.
So kann eine Zahlenfolge einen Test bestehen, jedoch in vielen anderen Durchfallen oder bei Untersuchung von Teilstücken einer
Folge von Zufallszahlen einige bestehen und andere nicht. Hier liegt vorallem das Problem vor, dass immer nur eine Endliche 
Folge vorliegt. Wirklicher Zufall allerdings kann nur bei einer unendlich langen Folge zu 100% überprüft werden.

Eine völlig andere Idee als bei herkömmlichen Tests, in denen jeweils Gewisse Kriterien überprüft werden, ist die Nutzung von 
Maschinellem Lernen (machine-learning). Dabei sind besonders Neuronale Netzwerke weit verbreitet und erbringen erstaunliche 
Ergebnisse in vielen Bereichen. Die Idee ist also, ein Neuronales Netzwerk zu nutzen um Pseudo ('pseudo random numbers'-PRN),- 
aber auch Echte Zufallszahlen ('true random numbers'-TRN) zu überprüfen und gegebenfalls versteckte Korrelationen zwischen den Daten aufzudecken. 
So soll deren Güte aufgrund der Vorhersagbarkeit der Zahlenfolgen (welche im Falle von binären Bitfolgen natürlich 
eigentlich bei 50% liegen sollte) überprüft werden.


## Was ist machine learning eigentlich?
Im machine learning gibt es verschiedene Disziplinen. Hier soll sich mit dem 'supervised learning' und besonders mit Neuronalen Netzwerken beschäftigt werden. Beim 'supervised learning' wird ein Problem durch einen Input und einen dazugehörigen markierten Output beschrieben. Als Beispiel kann hier eine Folge von Zufallszahlen genommen werden. Der Input könnten die ersten 5 Zahlen der Folge sein, der zugehörige Output die 6. Zahl der Folge. Ein anderes, weitaus bekannteres, Beispiel wäre die Klassifikation eines Bildes (also die Pixel als Inputs) in ein Bild einer Katze oder keiner Katze (Output). 
![bild1](../pascal/ki-katze.jpg)
[Bild Quelle](https://blog.iao.fraunhofer.de/spielarten-der-kuenstlichen-intelligenz-maschinelles-lernen-und-kuenstliche-neuronale-netze/)
Diese Paare von Inputs und Outputs werden auch Trainings-Set oder Trainings-Daten genannt. Das Ziel ist, dass das Neuronale Netzwerk, was im Prinzip nur eine komplizierte nichtlineare Funktion mit sehr vielen Parametern ist, die bekannten Inputs auf die zugehörigen Ouputs abbildet.
Um dies zu erreichen kann das Neuronale Netzwerk bzw. die Parameter der Netzwerk-Funktion mithilfe des 'Backpropagation'-Algorythmus optimiert werden, um die gewählten Trainings-Daten möglichst gut zu Beschreiben. 
Die Idee dahinter ist, wenn das Netzwerk genug Trainingsbeispiel gesehen/gelernt hat, sollte es ein grobes Verständnis besitzen was eine Katze ausmacht und dieses auf neue und unbekannte Inputs, also in diesem Fall Bilder, Anwenden können und diese hoffentlich richtig Klassifizieren.

Dies ist natürlich nur eine sehr kurze und oberflächliche Beschreibung. Es gibt viele verschiedene Arten von Netzwerken die für verschiedene Arten von Daten besser geeignet sind. Ausserdem ergeben sich besonders beim trainieren des Netzwerks weitere Probleme, wie das Überfitten, was im Prinzip die zu gute Beschreibung der Trainingsdaten aber eine dadurch schlechte Beschreibung von unbekannten Daten benennt. Dadurch ergibt sich besonders das Problem, wann das Training beendet werden sollte. Zudem ergeben sich weitere Spitzfindigkeiten beim Optimierungsprozess selbst, bei dem es viele verschiedene Algorithmen gibt.

In der Recherche zu diesem Projekt und besonders für ein tieferes Verständnis von Neuronalen Netzwerken waren die kostenlosen Kurse von [Adrew Ng.](https://www.youtube.com/watch?v=CS4cs9xVecg&list=PLkDaE6sCZn6Ec-XTbcX1uRg2_u4xOEky0) auf YouTube, sowie ältere [Vorlesungsskripte](http://cs229.stanford.edu/syllabus.html) besonders hilfreich.

## Idee und erste Tests
Bei den ersten Untersuchungen wurde sich besonders an dem Paper ['Learning from Pseudo-Randomness with an
Artificial Neural Network– Does God Play Pseudo-Dice?'](https://arxiv.org/ftp/arxiv/papers/1801/1801.01117.pdf) von Fenglei Fan und Ge Wang orientiert.
In dieser Arbeit wurden die Nachkommastellen der transzendente und somit auch irrationalen Zahl π auf ihre Zufälligkeit untersucht. Man geht davon aus, dass die Nachkommastellen der Zahl π vollkommen Zufällig sind und deshalb keine Periode enthalten dürften. Somit sollte man theoretisch, wenn man die Nachkommastellen der Zahl Pi erraten möchte eine 10%tige Chance haben, die richtige Ziffer (digit) voherzusagen. In der Arbeit selbst wurden die Nachkommastellen in eine Binäre Bit-Folge umgewandelt, indem alle Stellen mit Ziffern 0-4 zu 0 und alle Ziffern 5-9 zu 1 umgewandelt wurden. Laut der Arbeit sollte dies die Zufälligkeit erhalten und die Vorhersage mithilfe des Netzwerks vereinfachen.
Diese Binäre Bit-Folge wurde
Das erstaunliche Ergebnis dieser Arbeit ist, das

