<H1 align="center">Crud Structure</H1>
<p align="center">🚀 Project to create a Crud structure using Django for future references</p>

## Resources Used

* Django 5.0.2
* Python 3.10


## Create crudProject

<details>
 <summary>Click to show content</summary>

Initial project created with main structure, changing urls.py to add base.urls to add the packages.
 ```
django-admin startproject crudProject
 ```


### urls.py

```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
 path('admin/', admin.site.urls),
 path('', include('base.urls')),
]
```

### settings.py

```
INSTALLED_APPS = [
 'base.apps.BaseConfig',
 'django.contrib.admin',
 'django.contrib.auth',
 'django.contrib.contenttypes',
 'django.contrib.sessions',
 'django.contrib.messages',
 'django.contrib.staticfiles',
]
```

</details>






## Create base app

<details>
 <summary>Click to show content</summary>

Creation of a package that will be responsible for Crud's logic.

 ```
python manage.py startapp base
 ```


### models.py
Model that will be used to create tasks.

### admin.py
Mapping each model and registering it as a configuration that will be used on the admin page.

### urls.py

I have the route mapping.

The paths and respective views that will render.

```
 path('', TaskList.as_view(), name='tasks'),
 path('task/<int:pk>/', TaskDetail.as_view(), name='task'),
 path('task-create/', TaskCreate.as_view(), name='task-create'),
 path('task-update/<int:pk>/', TaskUpdate.as_view(), name='task-update'),
 path('task-delete/<int:pk>/', DeleteView.as_view(), name='task-delete'),
```

#### List

By default, when using createdviewname.as_view(), the path to find the html file will be based on modelname_actionname.html (task_list.html) or by changing this configuration through template_name in views.py.
```
path('', TaskList.as_view(), name='tasks'),
```

#### Create

The path to find the html file will be based on model_form.html name (task_form.html) or by changing this configuration through template_name in views.py.
```
path('task-create/', TaskCreate.as_view(), name='task-create')
```

#### Update

The path to find the html file will be based on model_form.html name (task_form.html) or by changing this configuration through template_name in views.py.

```
path('task-update/<int:pk>/', TaskUpdate.as_view(), name='task-update')
```

#### Delete

The path to find the html file will be based on the configuration through template_name in views.py.

```
path('task-delete/<int:pk>/', DeleteView.as_view(), name='task-delete')
```

</details>




## Create template 

<details>
 <summary>Click to show content</summary>

Directory responsible for storing the html pages that will be rendered.

By convention, within "template" project_name/view_name.html is used so that the framework recognizes the path.


### Views.py
Responsible for the view rendering and data flow controller.



```
class TaskList(ListView):
 model = Task
 context_object_name = 'tasks'
 template_name = 'base/task_list.html'
```

* model => Uses model as a reference for rendering the view
* context_object_name => It's just a human understandable variable name to access from models
* template_name = By default the path uses the suffix _list + model task name to search for the task_list.html file or using template_name to change this configuration

</details>
