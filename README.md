# elastic-deletebyquery

Just add to your package.json

```json
"dependencies": {
    "elastic-deletebyquery": "git@github.com:arielfr/elastic-deletebyquery.git"
}
```

or

```
npm install --save git+ssh://git@github.com:arielfr/elastic-deletebyquery.git
```

# Usage

You need to require the module. Then call the method and pass the client on the parameter.

Then it is just a SCROLL, so you can pass the options of the scroll the only option by default is the scroll = 30s.

If you leave empty the query, you are going to delete all the documents on the type

```javascript
var elasticsearch = require('elasticsearch'),
    elasticDeleteQuery = require('elastic-deletebyquery')

var client = new elasticsearch.Client({
    host: 'localhost:9200'
});

elasticDeleteQuery(client);

var options = {
    index: 'index',
    type: 'type'
}

//This will delete all
client.deleteByQuery(options, function(err, response){
    console.log('The elements deleted are: %s', response.elements);
});

var options = {
    index: 'index',
    type: 'type',
    body: {
        query: {
            term: {
                _id: 1
            }
        }
    }
}

//This will delete only the document with the id = 1
client.deleteByQuery(options, function(err, response){
    console.log('The elements deleted are: %s', response.elements);
})
```

If you want to see the parameters that scroll supports, just visit the [elasticsearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/2.3/search-request-scroll.html)