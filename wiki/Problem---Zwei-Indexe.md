## Problem: Zwei Indexe

Das Datum war in zwei Verschiedenen Indexen vorhanden, sollte aber für eine gemeinsame Auswertung verwendet werden. Zusätzlich war das Datum in beiden Indexen in zwei Verschiedenen Schreibweisen angegeben. Es musste aber für eine gemeinsame Auswertung in den gleichen Typ konvertiert werden.

### Lösung:

In beiden CSVs wurde jeweils das Datumsfeld geklont und ein neuer, in beiden Dateien gleicher Name vergeben. Wenn sowohl der Name eines Feldes als auch der Typ gleich sind, werden die zwei eigentlich unterschiedlichen Felder in einem Kibanaindex als ein Feld betrachtet und kann als Basis eines Diagramms dienen.
