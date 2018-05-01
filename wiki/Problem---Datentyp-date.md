## Problem: Datentyp 'date'

Die Datumsfelder lagen in den CSVs als Strings vor. Sie müssen aber um mit Kibana Histogramme zu erstellen im Datentyp 'Date' vorliegen.

### Lösung:

Man kann Strings in den Logstashfiles in ein Datum konvertieren, in dem man angibt, wie das vorhanden Datum im String aussieht. Dazu verwendet man Pattern wie zum Beispiel dd-MM-yyyy.

`date {`

`    match => [ "Date", "dd/MM/yyyy" ]`

`    target => "Date"`

`}`