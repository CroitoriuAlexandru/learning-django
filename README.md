# Steps for everything
<!-- install python on your system -->


## 1BaseProject



### install Flowbite 3

cd ./proj/theme/static_src
npm install flowbite

---- aditional settings tailwind config  ----
    darkMode: 'class',
    content: [
        "./node_modules/flowbite/**/*.js",
    ],
    plugins: [
        require('flowbite/plugin')
    ],

---- set static files directories in settings.py ----
STATICFILES_DIRS = [
    BASE_DIR / "theme/static",
    "theme/static_src/node_modules/flowbite/dist",
]

---- add script in base.html ----
<script src="{% static 'flowbite.min.js' %}"></script>



### install django-tailwind 2
pip install django-tailwind[reload]

---- INSTALLED_APPS ---- needs to be added for the init step
'tailwind',

python3 manage.py tailwind init

---- INSTALLED_APPS ---- add the initiated app with default name theme 
'theme',
'django_browser_reload'

---- MIDDLEWARE ---- add the initiated app in middleware
"django_browser_reload.middleware.BrowserReloadMiddleware",

---- Register the initiated app in settings ----
TAILWIND_APP_NAME = 'theme'

---- Add ip in INTERNAL_IPS ----
INTERNAL_IPS = [
    "127.0.0.1",
]

python3 manage.py tailwind install

Create templates folder and a base.html file in it
{% load static %}
{% load tailwind_tags %}
{% tailwind_css %}

--- add path for reload ---
from django.urls import include, path
urlpatterns = [
    ...,
    path("__reload__/", include("django_browser_reload.urls")),
]

---- add templates folder in settings ----
TEMPLATES = 
[ 
    {
        'DIRS': [BASE_DIR / 'templates'], # add templates folder
    } 
]

python3 manage.py tailwind start


### create project 1
python3 -m venv .venv 
source .venv/bin/activate
pip install django
django-admin startproject proj
cd proj
python3 manage.py migrate
python3 manage.py runserver

