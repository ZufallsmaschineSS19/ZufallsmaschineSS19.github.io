# Das Arduino-Experiment

## Ideenfindung
Zufallszahlen spielen im Alltag, in der Wissenschaft und der Informatik eine immer größer werdende Rolle. Da im allg. die vom Computer erzeugten Pseudo-Zufallszahlen nicht wirklich zufällig sind und damit vorhersagbar, wollten wir uns damit beschäftigen anhand eines physikalischen Aufbaus echte Zufallszahlen zu erzeugen.\
Unter den beiden Möglichkeiten der experimentellen Bestimmung von Zufallszaheln: der quantenmechanischen und der mittels Rauschen, haben wir uns für letztere entschieden.\
Diese arbeitet damit, dass aufgrund der schweren Vorhersgbarkeit von physikalischen Anfangsbedingungen, in einem System Rauschen entsteht das wiederun in Zufallszahlen umgewandelt werden kann.\
Da unsere Exprimentellen Möglichkeiten diesbezüglich sehr eingeschränkt waren und wir keinen zugang zu Hitech Instrumenten hatten, beschlossen wir einen möglichst einfachen, zu Hause umsetztbaren Aufbau umzusetzten.

## Versuchsaufbau

Mittels einer Zenerdiode als Rauschquelle, einem dazwischen geschalteten Verstärker und einem Arduino als Mikrokontroller haben wir dies mit dieser Schaltung umgesetzt.

Dazu haben wir benötigt:

In Original sieht das dann so aus:

## Durchfürung

## Messen des Rauschen des Arduino ADC

Da das Rauschen des Analog-Digital-Converters (ab jetzt ADC) anscheinend stärker als das Rauschen der Zenerdiode ist, bleibt uns nichts anderes übrig als dieses zu messen und zu schauen, wie zufällig es sich verhält. \
Zuerst betrachten wir den zeitlichen Verlauf des Signals direkt, was mit dem Serial-Plotter, des Arduino-Programs sehr leicht ist:
TODO: Bild des signals
Die x-Achse des Plots ist die Nummer des gesendeten Bytes und die y-Achse der Wert des Bytes. Wie man sieht schwankt der Wert nur um 1 bit nach oben und unten, und das relativ regelmäßig. Um dies zu quantifizieren könnte man eine Frequenzanalyse mittels Fouriertransformation machen, was hier aber der einfachheit halber ausgelassen wurde, außerdem haben wir uns davon keine wichtigen Informationen erhofft. Stattdessen haben wir ein Programm geschrieben, welches misst, wie lange das Signal braucht um von einem Wert zu einem anderen zu wechseln.

### Testen der Erhaltenen Zahlen

## Auswertung
