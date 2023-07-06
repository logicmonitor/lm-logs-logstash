[![Gem Version](https://badge.fury.io/rb/logstash-output-lmlogs.svg)](https://badge.fury.io/rb/logstash-output-lmlogs)

This plugin sends Logstash events to the [Logicmonitor Logs](https://www.logicmonitor.com) 

# Getting started

## Installing through rubygems

Run the following on your Logstash instance

`logstash-plugin install logstash-output-lmlogs`

## Minimal configuration
```
output {
    lmlogs {
        portal_name => "your company name"
        access_id => "your lm access id"
        access_key => "your access key"
    }
}
```
You would need either `access_id` and `access_id` both or `bearer_token` for authentication with Logicmonitor.



## Important options

| Option | Description| Default |
| --- | --- | --- |
| batch_size | Event batch size to send to LM Logs.| 100 | 
| message_key | Key that will be used by the plugin as the system key | "message" |
| lm_property | Key that will be used by LM to match resource based on property | "system.hostname" |
| keep_timestamp | If false, LM Logs will use the ingestion timestamp as the event timestamp | true |
| timestamp_is_key  | If true, LM Logs will use a specified key as the event timestamp | false |
| timestamp_key | If timestamp_is_key is set, LM Logs will use this key in the event as the timestamp | "logtimestamp"  |
| include_metadata  | If false, the metadata fields will not be sent to LM Logs  | true |

See the [source code](lib/logstash/outputs/lmlogs.rb) for the full list of options

The syntax for `message_key` and `source_key` values are available in the [Logstash Event API Documentation](https://www.elastic.co/guide/en/logstash/current/event-api.html)

## Known issues 
 - Installation of the plugin fails on Logstash 6.2.1.
 
 
 ## Contributing
 
 Bug reports and pull requests are welcome. This project is intended to
 be a safe, welcoming space for collaboration.
 
 ## Development
 
We use docker to build the plugin. You can build it by running  `docker-compose run jruby gem build logstash-output-lmlogs.gemspec `
