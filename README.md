<H1 align="center">Estrutura Crud</H1>
<p align="center">🚀 Projeto de criação de uma estrutura de Crud utilizando Django para referências futuras</p>

## Recursos Utilizados

* Django 5.0.2
* Python 3.10


## Criação do crudProject

<details>
  <summary>Clique para mostrar conteúdo</summary>
  
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

</details>






## Criação da base

<details>
  <summary>Clique para mostrar conteúdo</summary>
  
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

</details>




## Criação Template

<details>
  <summary>Clique para mostrar conteúdo</summary>
  
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

</details>







