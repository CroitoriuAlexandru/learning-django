
## Steps to start the 1BaseTailwindFlowbite project
cd 1BaseTailwindFlowbite/
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cd proj/
python3 manage.py migrate
python3 manage.py tailwind install

> **Note**  first start the tailwind process for the static folder to be generated
python3 manage.py tailwind start
python3 manage.py runserver


## step 3  install Flowbite 

> **Note**  install flowbite in npm
```
cd ./proj/theme/static_src 
npm install flowbite
```
> **Note**  aditional settings tailwind config  
```
darkMode: 'class', 
content: [ 
	"./node_modules/flowbite/**/*.js",
	], 
plugins: [ 
	require('flowbite/plugin')
],
```
> **Note** set static files directories in settings.py 
```
STATICFILES_DIRS = [ 
	BASE_DIR / "theme/static", "theme/static_src/node_modules/flowbite/dist", 
]
```
> **Note** add script in base.html 
```
<script src="{% static 'flowbite.min.js' %}"></script>
```

## step 2 django-tailwind
```
pip install django-tailwind[reload]
```
> **Note** add next app to INSTALLED_APPS in settings
```
'tailwind',
```
> **Note** Run the next command to initiate the theme app 
```
python3 manage.py tailwind init
```
> **Note** add next apps to INSTALLED_APPS in settings
```
'theme',
'django_browser_reload'
```
> **Note** add next middleware to MIDDLEWARE in settings
``` 
"django_browser_reload.middleware.BrowserReloadMiddleware",
```
> **Note** add tailwind app name in settings
```
TAILWIND_APP_NAME = 'theme'
```
> **Note**  set INTERNAL_IPS in settings 
```
INTERNAL_IPS = [ "127.0.0.1", ]
```
> **Note** install npm packages
```
python3 manage.py tailwind install
```
> **Note** Create templates folder and a base.html file in it 
```
{% load static %} 
{% load tailwind_tags %} 
{% tailwind_css %}
```
> **Note** add path for reload 
```
from django.urls import include, path 

urlpatterns = [ 
	path("__reload__/", 
	include("django_browser_reload.urls")), 
	]
```

> **Note** add templates folder in settings 
```
TEMPLATES = [ 
	{ 'DIRS': [BASE_DIR / 'templates'], # add templates folder } 
]
```
> **Note** run the process that watches for changes
```
python3 manage.py tailwind start
```
## step 1 create project
```
python3 -m venv .venv 
source .venv/bin/activate 
pip install django 
django-admin startproject proj 
cd proj 
python3 manage.py migrate 
python3 manage.py runserver
```
