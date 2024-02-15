<H1 align="center">Estrutura Crud</H1>
<p align="center">🚀 Projeto de criação de uma estrutura de Crud utilizando Django para referências futuras</p>

## Recursos Utilizados

* Django 5.0.2
* Python 3.10


## Criação do crudProject

Projeto inicial criado com estrutura principal, alterando urls.py para adicionar base.urls para adicionar os packages. 
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



## Criação da base

Criação de um pacote que será responsável pela lógica de Crud.

 ```
python manage.py startapp base
 ```


### models.py
Modelo que será utilizado para criação das tarefas.

### admin.py
Mapeando cada model e registrando como uma configuração que será utilizada na página de admin.
 
### urls.py

Possuí o mapeamento das rotas.

Os caminhos e as respectivas views que irá renderizar.

```
    path('', TaskList.as_view(), name='tasks'),
    path('task/<int:pk>/', TaskDetail.as_view(), name='task'),
    path('task-create/', TaskCreate.as_view(), name='task-create'),
    path('task-update/<int:pk>/', TaskUpdate.as_view(), name='task-update'),
    path('task-delete/<int:pk>/', DeleteView.as_view(), name='task-delete'),
```

#### List

Por default, ao utilizar nomedaviewcriada.as_view(), o caminho para achar o arquivo html usará como base nomedomodel_nomedaação.html (task_list.html) ou alterando essa configuração através de template_name em views.py.
```
path('', TaskList.as_view(), name='tasks'),
```

#### Create

O caminho para achar o arquivo html usará como base nomedomodel_form.html (task_form.html) ou alterando essa configuração através de template_name em views.py.
```
path('task-create/', TaskCreate.as_view(), name='task-create')
```

#### Update

O caminho para achar o arquivo html usará como base nomedomodel_form.html (task_form.html) ou alterando essa configuração através de template_name em views.py.

```
path('task-update/<int:pk>/', TaskUpdate.as_view(), name='task-update')
```

#### Delete

O caminho para achar o arquivo html usará como base a configuração através de template_name em views.py.

```
path('task-delete/<int:pk>/', DeleteView.as_view(), name='task-delete')
```

## Criação Template

Diretório responsável por armazenar as páginas htmls que serão renderizadas.

Por convenção, dentro de "template" é utilizado nome_do_projeto/nome_da_view.html para que framework reconheça o caminho.
 

### Views.py
Responsável pelo controller de renderização de views e fluxo de dados.



```
class TaskList(ListView):
    model = Task
    context_object_name = 'tasks'
    template_name = 'base/task_list.html'
```

* model => Utiliza model como referência para renderização da view
* context_object_name => É apenas um nome de variável compreensível para humanos para acessar a partir de modelos
* template_name = Por default o path utiliza o sufixo _list + nome do model task para procurar pelo arquivo task_list.html ou utilizando template_name para alteração dessa configuração 

# Resultado

## Index
<img src="https://cdn.discordapp.com/attachments/1046824853015113789/1207778478141874258/image.png?ex=65e0e25c&is=65ce6d5c&hm=bbeae0f7fe59d4c212c8960fa038612dc3f8505ec6d12797a79a868434c3e0d4&" alt="">

## Create/Update
<img src="https://cdn.discordapp.com/attachments/1046824853015113789/1207778941067206716/image.png?ex=65e0e2ca&is=65ce6dca&hm=f9055c95161be8dd7838685eb8c7370278311ec311bee78de56407e66cdfd066&" alt="">

