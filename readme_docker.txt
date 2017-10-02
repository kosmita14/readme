/etc/docker/daemon.json
{
    "graph": "/media/pi/ext250/docker_data",
    "log-driver": "fluentd",
    "log-opts": {
        "fluentd-async-connect": "true"
     }
}

sudo docker run -d -p 6379:6379 -v /media/pi/ext250/redisdata:/data redis
sudo docker run -d -p 1880:1880 -v /media/pi/ext250/nodered_data:/data mynodered


sudo docker run -d --rm --name myelastic -v /media/pi/ext250/elastic_data:/usr/share/elasticsearch/data -p 9200:9200 -p 9300:9300 elasticsearch
sudo docker run --rm -p 5601:5601 --link myelastic:myelastic-url -e ELASTICSEARCH_URL=http://myelastic-url:9200 -d kibana
sudo docker run -d --rm --net=host --cap-add SYS_PTRACE -v /proc:/host/proc:ro -v /sys:/host/sys:ro -v /var/run/docker.sock:/var/run/docker.sock -p 19999:19999 --privileged titpetric/netdata
sudo docker run -d --rm --net=host --log-driver=fluentd --log-opt tag=docker.netdata --cap-add SYS_PTRACE -v /proc:/host/proc:ro -v /sys:/host/sys:ro -v /var/run/docker.sock:/var/run/docker.sock -p 19999:19999 --privileged titpetric/netdata
docker build -t myfluentd:latest ./

sudo docker run -d -p 24224:24224 -p 24224:24224/udp --link myelastic:localhost --link some-rabbit -v /media/pi/ext250/fluentd_data:/fluentd/log myfluentd
docker run -d --rm -p 15672:15672 -p 5672:5672 --name some-rabbit --hostname localhost rabbitmq:management
docker run --rm -d --link some-rabbit --link myelastic:localhost mylogstash:latest
docker build -t mylogstash:latest ./



docker-compose up -d --scale some-logstash=10
docker-compose down

