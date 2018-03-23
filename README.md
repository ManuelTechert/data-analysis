# Datenanalyse über Verkehrsdaten und Unfallstatistiken in UK Mithilfe von Logstash, Elasticsearch und Kibana

## Daten

Daten wurden von folgenden Seiten heruntergeladen:

- https://www.kaggle.com/silicon99/dft-accident-data
- https://www.kaggle.com/sohier/uk-traffic-counts

## Anpassungen

Folgende Zeilen müssen in den Config Files durch den eigenen Pfad angepasst werden:

- uk_accidents.conf:

		Zeile 3:     path => "/Users/danie/Downloads/accidents/Accidents0515.csv"

		Zeile 62:    template => "/Users/danie/Downloads/accidents/elasticsearch_template_accidents.json"

- uk_traffic.conf:

		Zeile 3:     path => "/Users/danie/Downloads/traffic/Raw-count-data-major-roads.csv"

		Zeile 60:    template => "/Users/danie/Downloads/traffic/elasticsearch_template_traffic.json"

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

- `C:\Users\danie\Downloads\logstash-6.2.2\logstash-6.2.2\bin\logstash -f C:\Users\danie\Downloads\accidents\uk_accidents.conf`

- `C:\Users\danie\Downloads\logstash-6.2.2\logstash-6.2.2\bin\logstash -f C:\Users\danie\Downloads\traffic\uk_traffic.conf`

#### Kibana

Im Browser http://localhost:5601/ aufrufen:

- Unter `Index Patterns` Index `uk_accidents` anlegen
- Unter `Index Patterns` Index `uk_traffic` anlegen
- Unter `Saved Objects` `export.json` importieren

## Schlusswort

Das Projekt wurde von Daniel Pies, Thomas Pötz und Manuel Techert erstellt.
