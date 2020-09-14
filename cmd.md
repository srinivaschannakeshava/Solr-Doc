# solr cmds

- solr.cmd start - start the solr
- solr.cmd create -c <name> - create a core to hold the indexes
- solr.cm -e cloud - intuitive example mode to start solr cloud
- solr.cmd start -cloud -p 8984 -s example\cloud\node2\solr -z "localhost:2181,localhost:2182,localhost:2183" - start solr in cloud mode with zookeeper address
- solr.cmd start -c -p <portNumber> -z <zookeeperConnectionString> -s <pathOfcoreIfRestarting>
- solr create -c films -s 2 -rf 2   - create a core with core name film sharding - 2 and replicationfactor 2
- delete indexes in solr - {'delete': {'query': '*:*'}} in documents tab with documentType - Solr Command(raw xml or json)



# Solr query commads
- ``` facet=true&facet.field=directed_by_str&facet.field=genre_str ``` to get facet on multiple fields the query parameter
  > note to have search on string make sure the field type is string. if the type is text it starts spliting on space.
- ```facet=true&facet.range=initial_release_date&facet.range.start=NOW-20YEAR&facet.range.end=NOW&facet.range.gap=+1YEAR``` - range facet query example
- ```facet.pivot=genre_str,directed_by_str``` -pivot facet list the facet of director with genres
- ``` bin/solr delete -c films``` - delete collection

- https://lucene.apache.org/solr/guide/8_6/solr-control-script-reference.html - solr guide on installaction cmds

- starting a solr cloud
  - solr.cmd start -c -p 8983 -s C:\softwares\databases\solr-8.5.2\server\solr-cloud\node1                  - note the node1 folder should be present with solr.xml and zoo.cfg
  - solr.cmd start -c -p 8984 -s C:\softwares\databases\solr-8.5.2\server\solr-cloud\node2 -z localhost:9983
  - solr.cmd start -c -p 8985 -s C:\softwares\databases\solr-8.5.2\server\solr-cloud\node3 -z localhost:9983