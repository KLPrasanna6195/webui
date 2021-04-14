# webui

Webui is a django frame work project where there will be a web page for searching a word in the document which is present in database. If give search word is found in the document then it shows results of the word else it will send a message like 'no results found based on search word'.

Steps for installation and running the code:
1) webui (zip file)  is a django project. One need to install and unzip it.
2) place it in a folder and load the csv file(python_assesment(2).csv) into database. In this project i am using postgres database. 
3) Change user, name and password in the settings.py file in webui with your name, user and postgres database password.
4) open cmd and specify the folder path and run the django server.
5) steps to run django server, python manage.py makemigrations---> python manage.py migrate ----> python manage.py runserver then the server starts running at the http://127.0.0.1:8000/.
6) http://127.0.0.1:8000/search/ is the url for webui. Go to this url.
7) In the search button enter a word to search or mention it in a url parameter as ?NAME='<some word>'
8) click search button
9) page will be redirected to django rest framework will results if any else we will get no results as output.
