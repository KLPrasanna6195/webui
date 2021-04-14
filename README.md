# webui


Webui is a django frame work project where there will be a web page for searching a word in the document which is present in database. If give search word is found in the document then it shows results of the word else it will send a message like 'no results found based on search word'.

To run locally, do the usual:
Django Project Prerequisites python >= 2.5

Create a Python 3.6 virtualenv


Installation Creating the environment

Create a virtual python environment for the project. If you're not using virtualenv or virtualenvwrapper you may skip this step.

For virtualenvwrapper

open cmd and follow these steps:

pip install virtualenv/wrapper - win

mkvirtualenv {{ Env name }}

virtualenv {{ Env name }}

if django is not installed in your system. install django.

pip install django

mkdir <some name>  #for django projects

cd {{ directory name which is given above }}

 According to current project :
 
 django-admin startproject webui
 
cd webui

django-admin startapp search

then run the server and check any errors or there. 

Open settings file in Project and mention app name and rest_framework in Installed apps and made changes in databases according to our database user, name and password.

'''DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'XXXXXX',
        'USER': 'postgres',
        'PASSWORD':'XXXXXXXXXXXX',
        'HOST':'127.0.0.1',
        'PORT':'5432',
    }
}'''

In this project we are using static files so, we need to write below lines in settings.py file:
  
  '''STATIC_URL = '/static/'
STATICFILES_DIRS = [
    (os.path.join(BASE_DIR, 'static')),
]
STATIC_ROOT = (os.path.join(BASE_DIR, "staticfiles"))
'''
In project folder urls.py, make below changes:


'''from django.conf.urls import url,include

  urlpatterns = [
    url('', include('search.urls')),
]
'''
Create urls.py in application folder:

Do, required changes in Models.py, urls.py and views.py

**Models.py:**

'''from django.db import models

# Create your models here.
class searchModel(models.Model):
    id = models.IntegerField(primary_key=True)
    name = models.CharField(max_length=100, null=False, blank=False, unique=True)

    def __str__(self):
        return self.name

    class Meta:
        db_table = "assesment"'''
        
**
views.py:**

'''from rest_framework.decorators import api_view
from django.shortcuts import render
from rest_framework.response import Response
from rest_framework import status
from search.models import searchModel


@api_view(['get'])
def get_queryset(request):
    if request.method == "GET":
        query = request.GET.get('NAME')
        if query:
            match = searchModel.objects.filter(name__icontains=query).values('name').order_by('name')
            results = list(match)
            if results == []:
                return Response('no results found based on search word', status=status.HTTP_200_OK)
            else:
                return Response(match[:21], status=status.HTTP_200_OK)
        else:
            return render(request, 'search.html')'''

**urls.py:**

'''from django.conf.urls import url
from . import views

urlpatterns=[
    url('search/',views.get_queryset),

]'''

 Create a folder templates and create search.html file:
 
 use below code in search.html
 
 ** search.html:**
  
'''<form method="GET" action="get_queryset">
        {% csrf_token %}
        <div class="form- group">
            <div class="col- lg-5">
                <input type=" text" name="NAME" class=" form-control" placeholder="Enter Word to Search">
            </div>
            <label class="col- lg-2">
                <button type=" submit" class="btn btn- primary"> Search </button>
            </label>
        </div>

</form>'''

In postgres database copy python_assesment(2).csv file into a empty table.

run below line of code in psql prompt.

\COPY assesment(id,name) FROM 'C:\path\to\csv\file\python-assesment (1).csv' DELIMITER ',' CSV HEADER;


Run the following commands in cmd:

python manage.py makemigrations

python manage.py migrate

python manage.py runserver

Open browser to http://127.0.0.1:8000

open  http://127.0.0.1:8000/search/  search and word and get output.


Steps for installation and running the code:

1) webui (zip file)  is a django project. One need to install and unzip it.

2) place it in a folder and load the csv file(python_assesment(2).csv) into database. In this project i am using postgres database. 

3) Change user, name and password in the settings.py file in webui with your name, user and postgres database password.

4) open cmd and specify the folder path and run the django server.

5) steps to run django server, python manage.py makemigrations---> python manage.py migrate ----> python manage.py runserver then the server starts running at the 

6) http://127.0.0.1:8000/.

7) http://127.0.0.1:8000/search/ is the url for webui. Go to this url.

8) In the search button enter a word to search or mention it in a url parameter as ?NAME='<some word>'

9) click search button

10) page will be redirected to django rest framework will results if any else we will get no results as output.
