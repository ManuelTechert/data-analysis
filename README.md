# Datenanalyse über Verkehrsdaten und Unfallstatistiken in United Kingdom mithilfe von Logstash, Elasticsearch und Kibana

## Daten

Daten wurden von folgenden Seiten heruntergeladen:

- https://www.kaggle.com/silicon99/dft-accident-data
- https://www.kaggle.com/sohier/uk-traffic-counts

## Anpassungen

Folgende Zeilen müssen in den Config Files durch den Pfad zum Ordner angepasst werden:

- uk_accidents.conf:

		Zeile 3:     path => "<Pfad zum Ordner>/accidents/Accidents0515.csv"

		Zeile 62:    template => "<Pfad zum Ordner>/accidents/elasticsearch_template_accidents.json"

- uk_traffic.conf:

		Zeile 3:     path => "<Pfad zum Ordner>/traffic/Raw-count-data-major-roads.csv"

		Zeile 60:    template => "<Pfad zum Ordner>/traffic/elasticsearch_template_traffic.json"

## Installation

#### Docker

Folgende Befehle auf der Konsole ausführen:

- `docker run -d -p 9200:9200 -p 9300:9300 -it -h elasticsearch --name elasticsearch elasticsearch`

- `docker run -d -p 5601:5601 -h kibana --name kibana --link elasticsearch:elasticsearch kibana`

#### Logstash

Archiv herunterladen und entpacken:

- https://artifacts.elastic.co/downloads/logstash/logstash-6.2.2.zip

#### Elasticsearch

Folgende Befehle auf der Konsole ausführen:

- `<Pfad zum Ordner>\logstash-6.2.2\logstash-6.2.2\bin\logstash -f <Pfad zum Ordner>\accidents\uk_accidents.conf`

- `<Pfad zum Ordner>\logstash-6.2.2\logstash-6.2.2\bin\logstash -f <Pfad zum Ordner>\traffic\uk_traffic.conf`

#### Kibana

Im Browser http://localhost:5601/ aufrufen:

- unter `Index Patterns` Index `uk_accidents` ohne Timefilter anlegen
- unter `Index Patterns` Index `uk_traffic` ohne Timefilter anlegen
- unter `Index Patterns` Index `uk*` ohne Timefilter anlegen
- unter `Saved Objects` `export-kibana.json` importieren

## Schlusswort

Das Projekt wurde von Daniel Pies, Thomas Pötz und Manuel Techert erstellt.
