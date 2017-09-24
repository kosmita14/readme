#montowanie nowego dysku pod elastica
mount |grep nowy
sudo umount /dev/sdc1
sudo mount /dev/sdc1 /media/pi/nowy_dysk -t ntfs-3g -o uid=123,gid=132,umask=000

#przy problemach z odmontowaniem
fuser /media/pi/nowy_dysk

#info o dostepnych dyskach
sudo blkid
https://help.ubuntu.com/community/Fstab#File_System_Type


pi@mint /usr/share/logstash $ sudo bin/logstash-plugin update



#x-pack
https://www.elastic.co/guide/en/x-pack/current/installing-xpack.html#xpack-package-installation

#logtrail
https://github.com/sivasamyk/logtrail


#create index customer
curl -XPUT 'localhost:9200/customer?pretty'

#list all indexes
curl 'localhost:9200/_cat/indices?v'

#delete an index
curl -XDELETE 'localhost:9200/customer?pretty'

#index document
curl -XPUT 'localhost:9200/customer/external/1?pretty' -d '
{
  "name": "John Doe"
}'


#list document
curl -XGET 'localhost:9200/customer/external/1?pretty'

#mapping field
curl -XGET 'localhost:9200/logstash-2017.01.29/_mapping/field/*?pretty'

#get template
curl -XGET 'localhost:9200/_template?pretty'
curl -XGET 'localhost:9200/_template/logstash?pretty'

#delete template
curl -XDELETE 'localhost:9200/_template/nib*?pretty'


curl -XPUT 'localhost:9200/_template/logstash?pretty' -d '
{
    "order": 0,
    "version": 50004,
    "template": "logstash-*",
    "settings": {
      "index": {
        "refresh_interval": "5s"
      }
    },
    "mappings": {
      "_default_": {
        "numeric_detection": true,
        "dynamic_templates": [
          {
            "message_field": {
              "path_match": "message",
              "mapping": {
                "norms": false,
                "type": "text"
              },
              "match_mapping_type": "string"
            }
          },
          {
            "string_fields": {
              "mapping": {
                "norms": false,
                "type": "text",
                "fields": {
                  "keyword": {
                    "type": "keyword"
                  }
                }
              },
              "match_mapping_type": "string",
              "match": "*"
            }
          }
        ],
        "_all": {
          "norms": false,
          "enabled": true
        },
        "properties": {
          "@timestamp": {
            "include_in_all": false,
            "type": "date"
          },
          "geoip": {
            "dynamic": true,
            "properties": {
              "ip": {
                "type": "ip"
              },
              "latitude": {
                "type": "half_float"
              },
              "location": {
                "type": "geo_point"
              },
              "longitude": {
                "type": "half_float"
              }
            }
          },
          "@version": {
            "include_in_all": false,
            "type": "keyword"
          }
        }
      }
    },
    "aliases": {}
  }'
