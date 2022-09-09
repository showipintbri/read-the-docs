# Elasticsearch / Logstash / Kibana

## Elasticsearch API w/CURL
tcp/9200 is the default port.

**HTTP:**

```
curl http://localhost:9200
```

If you get an error: `curl: (52) Empty reply from server` this likely means you need to use `https`.

**HTTPS:**
```
curl https://localhost:9200
```

If you get an error about trusted certificates you can use the `-k` flag to tell CURL to ignore untrusted certificates.

**HTTPS, Ignore Untrusted Certificates:**
```
curl -k https://localhost:9200
```

If you get an error about the 'security realm', you'll need to add HTTP Basic Authentication to your command.

**HTTPS, Ignore Untrusted Certificates w/Authentication:**
```
curl -k -u elastic:[password] https://localhost:9200
```

**List Indexes:**
```
curl -k -u elastic:[password] -XGET "https://localhost:9200/_aliases?pretty=true"
```

**Delete Index:**
```
curl -k -u elastic:[password] -XDELETE "https://localhost:9200/[explicit_index_name]"
```

# References:
- [https://linuxhint.com/elasticsearch-delete-index-how-to/](https://linuxhint.com/elasticsearch-delete-index-how-to/)




# Troubleshooting

## Error: "high watermark"
Your storage is full beyond the configured "high watermark" (90%?). You need to manually delete indices.

1. List your indexes (wildcards accepted)
2. Delete individual indexes (wildcards NOT accepted)
