## try couchDB docker image on Suse Linux

#### download couchdb 3.2 from github to your mac

```
docker pull couchdb:3.2
docker save couchdb:3.2 > /Users/rupeshkumar/vw/VW-70257-couchDB/couchdb-3-2.tar
```
#### tar it and move to server 10.10.27.166

```
sudo docker load < couchdb-3-2.tar 
sudo docker run -p 5984:5984 -v /Users/rupeshkumar/vw/VW-70257-couchDB/couchdb-3-2-volume:/opt/couchdb/data -e COUCHDB_USER=admin -e COUCHDB_PASSWORD=admin  couchdb:3.2
```

#### Populate with initial databases

```
curl -X PUT http://10.10.27.166:6984/_users
curl -X PUT http://10.10.27.166:6984/_replicator
curl -X PUT http://10.10.27.166:6984/_global_changes
```

#### hot to stop docker container

```
sudo docker ps -a 
sudo docker stop <contianer-id>
```

![clouseau-search-plugin-enabled-couchdb](images/clouseau-search-plugin-enabled-couchdb.jpg)

### Question. How to setup coouchDb in cluster mode to support Full Text Search 
Are you sure cluster mode is required to support it, Do you have any official documentation link from couchdb site.

### Question : Why, I should not use CouchDB lucene search anymore. 
Answer : Because it is not supported in couchdb-3.2 . Reference link from official documentation is below. You should use Clouseau instead. And Clouseau also does not have very good future. It is supported untill java-8. It will not run on higher version.

1.8. Search Plugin Installation — Apache CouchDB® 3.2 Documentation 

### Question :  Do i still need full text search plug-in like  lucene and Clousseau in couchdb 3.2 or  Mongo-query support  is sufficient ?
May be not. Below screenshot depicts mongo-query search result with postman. Query filter can be passed under selector. run your test cases to become more confident. Changing your code to rely on mongo-query is better because it will be supported in long run and advance and new. Lecene is already dead and Clouseau is supported only till java-8 so dying very soon and its written in scala , it may need lot of RAM. 

Mongo query support : 1.3.6. /db/_find — Apache CouchDB® 3.3 Documentation 
