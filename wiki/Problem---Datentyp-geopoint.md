## Problem: Datentyp 'geopoint'

Um mit Kibana Heatmaps zu erzeugen, die auf einer Landkarte anzeigen sollen, wo mehr und wo weniger Unfälle passiert sind, müssen die Koordinaten des Punktes in einem besonderen 'Geo_Point' Datentyp vorliegen. In beiden Datensätzen war dies natürlich noch nicht der Fall. Die Koordinaten lagen nur in Form von zwei Floatwert Longitude und Latitude vor.

### Lösung:

Es wurde eine zusätzliche Konstruktion erstellt, die ein neues Felds erstellt. Die Werte von Longitude und Latitude wurden dann in zwei Subfelder des neuen Feld eingefügt. Danach wurde diese Konstruktion in den Geo_Point Typ konvertiert.

`mutate {`

`    add_field => { "[geo_location_accidents][location][lat]" => "%{Latitude}"`

`                   "[geo_location_accidents][location][lon]" => "%{Longitude}" }`

`}`