docker run --name my_solr -d -p 8983:8983 -t -v /media/pi/ext250/business_events:/opt/solr/mydata solr:7.1


docker exec -it --user=solr my_solr bin/solr create_core -c mycore

docker exec -it --user=solr my_solr bin/post -c mycore mydata/output_not_scrumbled_100.json


curl -X POST -H 'Content-Type: application/json' 'http://localhost:8983/solr/mycore/update/json/docs' --data-binary '
{
  "payload": "test 123"
}'

https://lucene.apache.org/solr/guide/6_6/uploading-data-with-index-handlers.html

curl -X POST -H 'Content-Type: application/json' 'http://localhost:8983/solr/mycore/update/json/docs' --data-binary '
{
  "id": "1",
  "title": "Doc 1"
}'

curl -X POST -H 'Content-Type: application/json' 'http://localhost:8983/solr/my_collection/update' --data-binary '
{
  "add": {
    "doc": {
      "id": "DOC1",
      "my_field": 2.3,
      "my_multivalued_field": [ "aaa", "bbb" ]   
    }
  },
  "add": {
    "commitWithin": 5000, 
    "overwrite": false,  
    "doc": {
      "f1": "v1", 
      "f1": "v2"
    }
  },

  "commit": {},
  "optimize": { "waitSearcher":false },

  "delete": { "id":"ID" },  
  "delete": { "query":"QUERY" } 
}'


curl -X POST -H 'Content-Type: application/json' 'http://localhost:8983/solr/my_collection/update' --data-binary '
[
  {
    "id": "1",
    "title": "Doc 1"
  },
  {
    "id": "2",
    "title": "Doc 2"
  }
]'

