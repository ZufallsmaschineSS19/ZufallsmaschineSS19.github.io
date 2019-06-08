# Untersuchung von Pseudo,- und Echten Zufallszahlen mithilfe von Neuronalen Netzwerken

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
Im machine learning gibt es verschiedene Disziplinen. Hier soll sich mit dem 'supervised learning' und besonders mit Neuronalen Netzwerken beschäftigt werden. Beim 'supervised learning' wird ein Problem durch einen Input und einen dazugehörigen markierten Output beschrieben. Als Beispiel kann hier eine Folge von Zufallszahlen genommen werden. Der Input könnten die ersten 5 Zahlen der Folge sein, der zugehörige Output die 6. Zahl der Folge. Ein anderes, weitaus bekannteres, Beispiel wäre die Klassifikation eines Bildes (also die Pixel als Inputs) ob eine Katze oder ein Hund dargestellt ist (Output). 
![bild1](../pascal/ki-katze.jpg)
[Bild Quelle](https://blog.iao.fraunhofer.de/spielarten-der-kuenstlichen-intelligenz-maschinelles-lernen-und-kuenstliche-neuronale-netze/)

Diese Paare von Inputs und Outputs werden auch Trainings-Set oder Trainings-Daten genannt. Ein grober Aufbau eines einfachen Netzwerks ist im oben dargstellten Bild zu sehen. Der grundlegende Baublock ist ein so genanntes Neuron (Im Bild oben die Kreise). Diese sind jeweils mit allen Neuronen der nächsten Ebene verbunden. In einem Neuron wird eine gewichtete Summe über alle Inputs (auch Aktivierungen) aus der vorherigen Ebene gebildet und mit einer [Aktivierungs-Funktion](https://medium.com/the-theory-of-everything/understanding-activation-functions-in-neural-networks-9491262884e0), z.B. Sigmoid oder [ReLu](https://www.kaggle.com/dansbecker/rectified-linear-units-relu-in-deep-learning), zur nächsten Ebene transferriert und dort wieder alle Aktivierungen der voherigen Ebene als Inputs für die einzelnen Neuronen genutzt. Dabei werden alle Ebenen bei denen es sich nicht um die Input oder Output Ebene handelt als 'verborgene' Ebenen (hidden layers) bezeichnet.

Das Ziel ist, dass das Neuronale Netzwerk, was im Prinzip nur eine komplizierte nichtlineare Funktion mit sehr vielen Parametern ist, die bekannten Inputs auf die zugehörigen Ouputs abbildet.
Um dies zu erreichen kann das Neuronale Netzwerk bzw. die Parameter der Netzwerk-Funktion mithilfe des ['Backpropagation'-Algorithmus](http://neuralnetworksanddeeplearning.com/chap2.html) optimiert werden, um die gewählten Trainings-Daten möglichst gut zu Beschreiben. 
Die Idee dahinter ist, wenn das Netzwerk genug Trainingsbeispiel gesehen/gelernt hat, sollte es ein grobes Verständnis besitzen was eine Katze und einen Hund ausmacht und dieses auf neue und unbekannte Inputs, also in diesem Fall Bilder, Anwenden können und diese hoffentlich richtig Klassifiziert.

Dies ist natürlich nur eine sehr kurze und oberflächliche Beschreibung. Es gibt viele verschiedene Arten von Netzwerken die für verschiedene Arten von Daten besser geeignet sind. Ausserdem ergeben sich besonders beim trainieren des Netzwerks weitere Probleme, wie das Überfitten, was im Prinzip die zu gute Beschreibung der Trainingsdaten aber eine dadurch schlechte Beschreibung von unbekannten Daten benennt. Dadurch ergibt sich besonders das Problem, wann das Training beendet werden sollte. Zudem ergeben sich weitere Spitzfindigkeiten beim [Optimierungsprozess](https://towardsdatascience.com/types-of-optimization-algorithms-used-in-neural-networks-and-ways-to-optimize-gradient-95ae5d39529f) selbst, bei dem es viele verschiedene Algorithmen gibt.

In den folgenden Kapiteln wird davon ausgegangen, dass ein grundlegendes Verständnis von dem Aufbau eines Neuronalen Netzwerks bekannt ist.
In der Recherche zu diesem Projekt und besonders für ein tieferes Verständnis von Neuronalen Netzwerken waren die kostenlosen Kurse von [Adrew Ng.](https://www.youtube.com/watch?v=CS4cs9xVecg&list=PLkDaE6sCZn6Ec-XTbcX1uRg2_u4xOEky0) auf YouTube, sowie [Vorlesungsskripte](http://cs229.stanford.edu/syllabus.html) besonders hilfreich.


## Idee und erste Tests
Bei den ersten Untersuchungen wurde sich besonders an dem Paper ['Learning from Pseudo-Randomness with an
Artificial Neural Network– Does God Play Pseudo-Dice?'](https://arxiv.org/ftp/arxiv/papers/1801/1801.01117.pdf) von Fenglei Fan und Ge Wang orientiert.
In dieser Arbeit wurden die Nachkommastellen der transzendenten und somit auch irrationalen Zahl π auf ihre Zufälligkeit untersucht. Man geht davon aus, dass die Nachkommastellen der Zahl π vollkommen Zufällig sind und deshalb keine Periode enthalten dürften. Somit sollte man theoretisch, wenn man die Nachkommastellen der Zahl Pi erraten möchte eine 10%tige Chance haben, die richtige Ziffer (digit) voherzusagen. 

In der Arbeit wurden die Nachkommastellen in eine Binäre Bit-Folge umgewandelt, indem alle Stellen mit Ziffern 0-4 zu 0 und alle Ziffern 5-9 zu 1 umgewandelt wurden. Laut der Arbeit sollte dies die Zufälligkeit erhalten und die Vorhersage mithilfe des Netzwerks vereinfachen.
Diese Binäre Bit-Folge wurde nun in ein Trainings-Set umgewandelt, indem jeweils 6 Nachkommastellen als Input und die 7. als Output verwendet wurden. Es wurde ein relatives kleines Netzwerk mit 2 verborgenen Ebenen mit 30 und 20 Neuronen und die ersten 40,007 Nachkommastellen als Trainings-Set genutzt.

Ein Ergebnis dieser Arbeit ist, dass das Netzwerk nach dem Trainings-Prozess (mit 40 Epochen) mit 51%ger Wahrscheinlichkeit die richtige 7. Nachkommastelle auf dem Trainings-Set vorhersagt. Bei genauerer Überlegung ist dies jedoch nicht verwunderlich, denn umso größer ein Netzwerk, desto mehr Möglichkeiten bestehen, dass sich die Parameter des netzwerks beim Training gerade so anpassen, dass sie das gesamte Trainings beschreiben können. So sollte, wenn ein besonders großes (bzw. tiefes) Netzwerk mit vielen Neuronen und Ebenen genutzt wird, es möglich sein, auf dem Trainings-Set weit über 50% richtige vorhersagen zu erreichen. Dies sagt allerdings nicht viel über die Zufälligkeit der Folge aus, da die eigentlich interessanten Vorhersagen auf einem Daten-Set relevant sind, das nicht für den Trainingsprozess genutzt wurde, da an ihm erkannt werden kann, ob das gelernte verallgemeinert werden kann. Ist dies nicht der Fall spricht davon, dass das Trainings-Set überfitted wurde und was in diesem Fall anscheinend auch eingetreteten ist, da auf einem Test-Set der Nachkommastellen 100,000-1,000,007 nur durchschnittlich 50.1% der Vorhersagen richtig waren. Auf einem Test-Set der Nachkommastellen 999,999-9,999,006 wurden ebenso nur 50.02% richtige vorhersagen getroffen.

Um die zuvor beschriebene Vermutung zu bestätigen wurde versucht die Ergebnisse aus der Arbeit zu reproduzieren. Hierzu wurde die Programmiersprache [Python](https://www.python.org/) und dort die Bibliothek [Pytorch](https://pytorch.org/) verwendet, welche eine relativ einfache Implementation von Netzwerken und des Trainings ermöglicht.
Zunächst wurden die Nachkommastellen von π [hier](https://stuff.mit.edu/afs/sipb/contrib/pi/) heruntergeladen und in ein passendes Format gebracht.


