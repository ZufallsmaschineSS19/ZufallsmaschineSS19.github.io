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
Zuerst betrachten wir den zeitlichen Verlauf des Signals direkt, was mit dem Serial-Plotter, des Arduino-Programs sehr leicht ist:\
TODO: Bild des signals \
Die x-Achse des Plots ist die Nummer des gesendeten Bytes und die y-Achse der Wert des Bytes. Da mit einer bestimmten Frequenz (9600 Bps) Bytes gesendet werden, ist die Zahl auf der x-Achse proportional zur vergangenen Zeit. Wie man sieht schwankt der Wert nur um 1 bit nach oben und unten, und das relativ regelmäßig. Um dies zu quantifizieren könnte man eine Frequenzanalyse mittels Fouriertransformation machen, was hier aber der einfachheit halber ausgelassen wurde, außerdem haben wir uns davon keine wichtigen Informationen erhofft. \ Stattdessen haben wir ein Programm geschrieben, welches misst, wie lange das Signal braucht um von einem Wert zu einem anderen zu wechseln. Das sieht dann wie folgt aus:\
![Zeitdifferenz](timer_input_change_neu.png)
Nun sieht das jetzt noch weniger zufällig aus, sondern genau nach dem Gegenteil von Zufall: Periodizität. Beim genaueren Betrachten der Werte fällt allerdings auf, dass das Signal nicht exakt periodisch ist und es Abweichungen bei den wenig signifikanten, also den hinteren Stellen der Zahlen gibt. Das könnte ein zufälliges Hintergrundrauschen sein, aus dem man zufallszahlen herausbekommen könnte. \ Also wird der gesendete Wert auf 8 bit trunkiert, d.h. die hinteren 8 Bits der Binärdarstellung der Zahl werden benutzt, der Rest wird verworfen. 8 bit ist hier recht willkürlich, die ganze Zahl ist eine unsigned long Variable mit 32 bit, aber 8 bit sind eben genau ein Byte, was berechnen von Datenraten einfacher macht. Diese 8 bit der Zeitmessung werden nun über die serielle Schnittstelle an den Computer weitergegeben, wo sie gespeichert werden kann. Die gesendeten Bytes sehen dann so aus: \
TODO: Bild des "Rauschen" \
Das sieht schon mehr nach gewünschtem Rauschen aus, sehr unvorhersagbar. Nun wurden ca. 1000 aufeinanderfolgende Bytes gespeichert und um die Gleichverteilung zu überprüfen ein Histogramm angefertigt: \
![](histogram-page-001.jpg)
Hier sieht man, wie häufig welche Zahlen in dem Datensatz vorkommen. Wenn es sich um gleichverteiltes Rauschen handeln sollte, müssten alle Bins gleich besetzt sein, also alle Balken gleich hoch. Dies ist aber offensichtlich nicht der Fall, es gibt sogar viele ganz leere Bins. Das zeigt uns erstmal, dass die Werte der Bytes überhaupt nicht gleichverteilt ist und so lässt sich auch vermuten, dass sie nicht zufällig sind. \
Wenn man die Zahlen näher betrachtet, fällt auf, dass von 256 Werten (8 Bit in Dezimal) nur 26 verschiedene Werte erhalten werden

### Testen der Erhaltenen Zahlen

## Auswertung
