sudo systemctl start rabbitmq-server.service

http://localhost:15672/#/
guest / guest

curl -u guest:guest http://localhost:15672/api/exchanges/%2f/my_exchange/ |jq
curl -u guest:guest http://localhost:15672/api/exchanges |jq '.[] | .name'
curl -u guest:guest http://localhost:15672/api/exchanges |jq '.[] | {name, message_stats: .message_stats.publish_in}'

curl -u guest:guest http://localhost:15672/api/queues |jq |less
curl -u guest:guest http://localhost:15672/api/queues/%2f/fluentd |jq
curl -u guest:guest http://localhost:15672/api/queues/%2f/fluentd |jq

curl -u guest:guest http://localhost:15672/api/connections |jq '.[] | {client_properties}'
curl -u guest:guest http://localhost:15672/api/consumers |jq
