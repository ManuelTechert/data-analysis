# data-analysis


Daten von https://www.kaggle.com/silicon99/dft-accident-data

Anpassungen in den Files:
	uk_accidents_geo.conf:
		Zeile 3:     path => "/Users/danie/Downloads/accidents/Accidents0515.csv"
		Zeile 62:    template => "/Users/danie/Downloads/accidents/elasticsearch-template.json"

docker run -d -p 9200:9200 -p 9300:9300 -it -h elasticsearch --name elasticsearch elasticsearch

docker run -d -p 5601:5601 -h kibana --name kibana --link elasticsearch:elasticsearch kibana

https://artifacts.elastic.co/downloads/logstash/logstash-6.2.2.zip
	downloaden und entpacken

C:\Users\danie\Downloads\logstash-6.2.2\logstash-6.2.2\bin\logstash -f C:\Users\danie\Downloads\accidents\uk_accidents_geo.conf

http://localhost:5601/
	Index "uk_accidents_geo" anlegen
	export.json importieren
