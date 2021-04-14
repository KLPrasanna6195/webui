# webui

Webui is a django frame work project where there will be a web page for searching a word in the document which is present in database. If give search word is found in the document then it shows results of the word else it will send a message like 'no results found based on search word'.

Steps for installation and running the code:
1) webui (zip file)  is a django project. One need to install and unzip it.
2) place it in a folder and load the csv file(python_assesment(2).csv) into database. In this project i am using postgres database. 
3) open cmd and specify the folder path and run the django server.
4) http://127.0.0.1:8000/search/ is the url for webui. 
5) In the search button enter a word to search or mention it in a url parameter as ?NAME='<some word>'
6) click search button
7) page will be redirected to django rest framework will results if any else we will get no results as output.
