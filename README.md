# Lab workbook
## Guide
[Guide](https://adobe-my.sharepoint.com/personal/aponnusa_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=AYTGtSVjzDzIvYcz8ZvBF6m5YNTWFyNMQhTIAcAaQMY%3d&docid=2_1388328616c604e549804b28d667753fe&rev=1)

## Slides
[Lab Slides](https://www.dropbox.com/s/wry66jv0ks67ia9/L4300.pdf?dl=0)

# Troubleshooting Guide
We have put together a list of potential issues you might run into with recommendations on how you can identify the problem or workaround it. This list will hopefully shrink with time ;)

## AEM Issue

### Publisher (localhost:4503) not working
* On visiting [http://localhost:4503](http://localhost:4503), if the page says startup in progress give a few moments
* Open the termninal and type 
* `cd ~/aemcommunities/6.3/publish`
* `java -XX:MaxPermSize=256m -Xmx1024M -Dsling.run.modes=publish -jar cq-publish-4503.jar`

### Author (localhost:4502) not working
* On visiting [http://localhost:4502](http://localhost:4502), if the page says startup in progress give a few moments
* Open the termninal and type 
* `cd ~/aemcommunities/6.3/author`
* `java -XX:MaxPermSize=256m -Xmx1024M -Dsling.run.modes=publish -jar cq-author-4502.jar`

### Site Not published
* Publish the site a gain
* Wait for the green dialog
* This could be a latency issue, and we have no other choice but to wait

### Site Edit not being saved
* Edit the site again
* Click the save button
* In case of error there will be a red dialog with error details (could be config issues or missing fields)
* If not able to resolve the issue, edit the existing sample or a different site

## UGC Issues, No Sample Content

### Check Solr Status
* [http://localhost:8983/solr/](http://localhost:8983/solr/)

### Restart Solr
* Open cygwin and paste the commands
* `curl http://localhost:8983/solr/communities/update -H "Content-type: text/xml" --data-binary '<delete><query>*:*</query></delete>'`
* `curl http://localhost:8983/solr/communities/update -H "Content-type: text/xml" --data-binary  '<commit />'`

### Reset Solr
* Open cygwin and type
* `curl -s -u admin:admin  -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex`

### Check mongo
* Check if mongo process is running, type the following command in terminal
* `ps -ef | grep -i mongod | grep -v grep`
* If no result, then start mongo using the command `mongod --dbpath ~/aemcommunities/6.3/mongo`
