## <a name="Daten"></a>Daten

Daten wurden von folgenden Seiten heruntergeladen:

* [Unfallstatistiken](https://www.kaggle.com/silicon99/dft-accident-data)
* [Verkehrsdaten](https://www.kaggle.com/sohier/uk-traffic-counts)

## Notwendige Änderungen der Config-Files

Logstash akzeptiert nur [absolute Pfade](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-file.html#plugins-inputs-file-path) zu den Daten.
Aus diesem Grund müssen folgende Zeilen in den Config Files durch den lokalen Pfad zum Ordner ersetzt werden:

* uk_accidents.conf:

	* Zeile 3:     `path => "<Pfad zum Ordner>/accidents/Accidents0515.csv"`

	* Zeile 62:    `template => "<Pfad zum Ordner>/accidents/elasticsearch_template_accidents.json"`

* uk_traffic.conf:

	* Zeile 3:     `path => "<Pfad zum Ordner>/traffic/Raw-count-data-major-roads.csv"`

	* Zeile 60:    `template => "<Pfad zum Ordner>/traffic/elasticsearch_template_traffic.json"`

## Installation

#### Docker

Elasticsearch und Kibana werden in Docker-Containern ausgeführt. Docker kann über folgenden [Link](https://www.docker.com/get-docker) heruntergeladen und installiert werden.
Nachdem Docker gestartet wurde, müssen folgende Befehle auf der Kommandozeile ausgeführt werden:

* `docker run -d -p 9200:9200 -p 9300:9300 -it -h elasticsearch --name elasticsearch elasticsearch`

* `docker run -d -p 5601:5601 -h kibana --name kibana --link elasticsearch:elasticsearch kibana`

#### Logstash

Logstash läuft nicht in einem Docker-Container, sondern kann [hier](https://artifacts.elastic.co/downloads/logstash/logstash-6.2.2.zip) heruntergeladen werden.

Die Unfallstatistik- und Verkehrsdaten sind über die zuvor erwähnten [Links](#Daten) herunterzuladen und in die entsprechenden Ordner \accidents bzw. \traffic zu verschieben. Anschließend können die Daten über die nachfolgenden Befehle in Elasticsearch eingefügt werden:

* `<Pfad zum Ordner>\logstash-6.2.2\logstash-6.2.2\bin\logstash -f <Pfad zum Ordner>\accidents\uk_accidents.conf`

* `<Pfad zum Ordner>\logstash-6.2.2\logstash-6.2.2\bin\logstash -f <Pfad zum Ordner>\traffic\uk_traffic.conf`

#### Kibana

Im Browser http://localhost:5601/ aufrufen:

* unter `Index Patterns` Index `uk_accidents` ohne Timefilter anlegen
* unter `Index Patterns` Index `uk_traffic` ohne Timefilter anlegen
* unter `Index Patterns` Index `uk*` ohne Timefilter anlegen
* unter `Saved Objects` `export-kibana.json` importieren
