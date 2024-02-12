# Atlas Search Server

This Search Server code was initially written to support the article
("How to Build a Search Service in Java with MongoDB")[TBD] and video[TBD].

It uses the `jettyRun` target and searches the `movies_index`. The search
server code lives under `server/`

To run the search server locally, follow these steps:

* Add the [sample collections](https://www.mongodb.com/docs/atlas/sample-data/) to your Atlas cluster
    * If you're not already an Atlas user, [get started with Atlas](https://www.mongodb.com/docs/atlas/getting-started/)
* [Create an Atlas Search index](https://www.mongodb.com/docs/atlas/atlas-search/tutorial/create-index/) on the `movies` collection, named `movies_index`, using the index
  configuration below.
* `cd server/` - work within the server directory.
* Run the search service:
  `ATLAS_URI="<<insert your connection string here>>" ./gradlew jettyRun`
* Visit [http://localhost:8080](http://localhost:8080)

`movies_index` index configuration (JSON):
```
{
  "analyzer": "lucene.english",
  "searchAnalyzer": "lucene.english",
  "mappings": {
    "dynamic": true,
    "fields": {
      "cast": [
        {
          "type": "token"
        },
        {
          "type": "string"
        }
      ],
      "genres": [
        {
          "type": "token"
        },
        {
          "type": "string"
        }
      ]
    }
  }
}
```

_id: {
$toString: "$_id"
}

