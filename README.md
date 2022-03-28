# Django_Gunicorn_Nginx_MariaDB_Volume_Docker
Django Gunicorn Nginx MariaDB Volume StaticFiles Docker


python.exe -m pip install --upgrade pip 


virtualenv -p python3 .venv
source ~/.venv/bin/activate   

python -m venv env 
.\env\Scripts\activate


pip install django gunicorn
django-admin startproject config
tree
mv config app


cd app
python3 manage.py runserver


django-admin startproject web .

web>views.py :
from django.http import HttpResponse
def index(request):
          return HttpResponse("This is django ! ")

app>urls.py:
from web.views import home

urlpatterns = [
    path('', home),
    path('admin/', admin.site.urls),
    ]


app>settings.py:

add 'web', to INSTALLED_APPS = []



gunicorn -b 0.0.0.0:8000 config.wsgi


app>settindgs.py:
add ..

STATIC_URL = 'static/'
STATIC_ROOT = BASE_DIR.parent / 'static'

MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR.parent / 'media'

python manage.py collectstatic



config>urls.py:

from django.conf import settings
from django.conf.urls.static import static



export DJANGO_SUPERUSER_PASSWORD = Aa123456


