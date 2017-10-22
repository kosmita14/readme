curl 'localhost:9600/_node/stats/pipeline' | jq '[.pipeline.plugins.filters]' | jq '.[]' | jq '.[] | {id, duration: .events.duration_in_millis}

