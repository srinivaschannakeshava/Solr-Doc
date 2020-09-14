# Apache Solr

## Why Solr?

- Advanced Full text search capabilities
- Optimized for high volume web traffic
- standards based open interfaces - XML,JSON and http
- comprehensive HTML administration Interfaces
- Server statistics exposed over JMX for monitoring
- Near Real-time indexing
- Flexible and Adaptable with XML xonfiguration
- Extensible Plugin architecture
- A real data schema, with numeric types, Dynamic Fields, Unique Keys
- Faceted Search and Filtering
- Highly configurable and user extensible caching
- performance optimizations
- multiple search indices
- ## Scalability via solrcloud
- Linear Scalble , auto index replication, auto failover and recovery with no single point of failure
- Centralized Apache Zookeeper based configuration
- Automated distributed indexing/sharding
- near real-time indexing with immediate push based replication
- transaction log ensures no updates are lost even if the documents are not yet indexed to disk
- Automated query failover, index leader election adn recovery in case of failure

## Solr Architecture

- Lucene 
    - Open source search and indexing engine
    - works with any document which has fields that can be extracted and indexed
    - It has a specific syntax 
- Solr
  - Serverization of lucene
  - opensource enterprise search platform
  - Flexible and customizable
  - RESTful
  - Multiple search features
  - Supports replication and shards

## Solr Configuration

## solr query tab
    - q -the query
    - fq - filter query
    - sort - for sorting
    - star, rows - start is offset of returned result, row contols result returned i.e they are like pagination 
    - fl - specifies which fields to be returned
    - wt - response eriter json/xml response
    - indent - return result with proper indentation
    - debugquery- use augmente debug info for programmer/admin
    - dismax- enable dismax query parser 
    - edismax- enable the extende query parser
    - hl- highliting the query response
    - facet enables faceting,the arrangement of search result into category based on indexed terms
    - spatial Enable using location data for use in spatial or geospatial searches
    - spellcheck - enable spellcheck ,while provides inline query suggestions

- Solr document
  - Basic unit of information, set of data that describes something made up of fields
  - Json/xml representation i.e solr understands
  - schema field atributes
    > ex:- <field name="description" type="text_general" indexed="true" stored="true"> 
    - Name: field name
    - Type: field type as declared in <types> section
    - Indexed: true if idexed(searchable|sortable)
    - stored: true if retrievable
    - compressed: false store using gzip compression
    - multivalued: true if multiple values per document
    - Required: Instructs Solr to reject if missing
    - DocValues: If true, the value of the field will be put in column oriented DocValues structure
    - OmitNorms: true omits the norms associated with field
    - TermVectors: true to store the term vector for a given vector
    - TermPositions: store position info wiht the term vector
    - TermOffsets: Store offset info with term vector
    - default: value if none providing on adding document
  - > Note: you can find more info on properties to be enabled in schema based on use case [here](https://lucene.apache.org/solr/guide/6_6/field-properties-by-use-case.html)
  - Schema.xml - contains details about document fields and how to treat when documents added to or queried from the index

- solrconfig.xml
  - It contains the parameters to configure solr core 
  -  XML statements sets the following config
     -  Index Configuration
     -  Query
     -  Caching
     -  Event Listners
     -  Request Handlers
     -  Request Dispatchers
     -  Highlighter Plugin config
     -  Admin Gui section
  - Indexing
    - Adding content to a Solr Index If necessary modifying it and making it searchable

- Relevance- Is the degree to which a query response satisfies the user who is searching for information
- 2 concepts related to relavance
  - Precision - Percentage of documents in the returned results that are relavant
  - Recall - % of doc not relevant to search

- query event - q
  - text search
- filter query - fq
  - applied to restrict superset results
  - drill down without affecting score
    - most relevant doc at the top
  - useful for performance of complex queries
  - can specify multiple fq
  - ex: - course-author:"Jan-Erik Sandberg" OR "Xavier Morera"
- sorting
  - ex: coursetitle asc , coursetitle desc
- start, rows
  - start is the offset in the query result
  - rows determines how many documents to be returned
- fl - fields to be returned
  - default *
  - can include score
  - seperate with comma or space
  - results of functions can be included
  - recomended to avoid returning always everything
  - ex:- title,score,courseid
- df - default search field
  - only takes effect if qf not dwfinwd
    - dismax and edismax
    - overides defnition of a default field in scema.xml
- wt
  - response writer
- indent
  - used to format
- debug query
  - augment query response with ebug info
  - includes explain info for each document hiy
  - maily meant for administrator or programmer
- query parser
  - component responsible for parsing he textual query and converting to a lucene query object
  - three main built
    - standard
    - DisMax
    - eDisMax
  - Dismax
    - Maximum Disjunction
    - Designed to process simple phrases
    - Has advanced searching capabilities - different weight or boosts
  - eDisMax
    - Extended dismax
    - Improved version of Dismax
    - terms 
      - mm - minimum match
  - Highlighting
  - facet
    - Arrangement of search result into categories
      - based on indexed terms
      - Include numerical count
    - Allows users to drill down and narrow results
    - can be used to ge the facets based on range
    - 
  - spatial search
    - location search - called spatial or geo-spatial search
    - units in km , points of latitude/logitude
    - sort or score/boost by distance
    - also bound by shape
  - spellcheck
    - provide inline query suggestions based on other similar terms
  - synonyms
   - word or phraes that mean the same
   - match string of tokens and replace with other string of tokens
   - specify the synonyms in a file - synonym.txt
 - stemming
   - reducing a word to a shorter base form
   - stemming helps increase recall but makes your index much bigger
 - lemmatisation
   - exapnding a root word to all its various forms
 - stop words
   - discard common words
   - standard english stop words included in the list - ex: a an, and, are, as ,at
   - specify in a file -> stopwords.txt
   - solr.StopFilterFactory

 - Request Handler
   - they define the logic for any executed request


## Dockerizing solr notes

- solr cmds 
  - solr -e cloud --> start solr cloud example mode
  - solr -c 




> Notes
- Pivot Facet -also known as "decision trees", allowing two or more fields to be nested for all the various possible combinations.
  ex: Using the films data, pivot facets can be used to see how many of the films in the "Drama" category (the genre_str field) are directed by a director.
- SolrJ is a Java-based client for interacting with Solr
- https://lucene.apache.org/solr/guide/8_6/solr-control-script-reference.html - solr guide on installaction cmds


## Solr Cloud
- SolrCloud is designed to provide a highly available, fault tolerant environment for distributing your indexed content and query requests across multiple servers.
- When a document is sent to a Solr node for indexing, the system first determines which Shard that document belongs to, and then which node is currently hosting the leader for that shard. The document is then forwarded to the current leader for indexing, and the leader forwards the update to all of the other replicas.
- Types of Replicas
  - NRT - nearRealTime
  - TLOG
  - PULL
- There are three combinations of replica types that are recommended:
  - All NRT replicas - Use this for small to medium clusters, or even big clusters where the update (index) throughput is not too high
  - All TLOG Replicas - Use this combination if NearRealTime is not needed and the number of replicas per shard is high
  - TLOG replicas plus PULL replicas
- Limiting Which Shards are Queried
  - http://localhost:8983/solr/gettingstarted/select?q=*:*&shards=shard1 
  - http://localhost:8983/solr/gettingstarted/select?q=*:*&shards=shard1,shard2
- Aliases
  - SolrCloud has the ability to query one or more collections via an alternative name. These alternative names for collections are known as aliases, and are useful when you want to:
    - Atomically switch to using a newly (re)indexed collection with zero down time (by re-defining the alias)  
    - Insulate the client programming versus changes in collection names
    - Issue a single query against several collections with identical schemas
  - 2 types of aliases
    - Standard Aliases
    - Routed Aliases


# Taking solr to prodution
- 