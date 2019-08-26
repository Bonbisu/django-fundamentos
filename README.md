# Django - Fundamentos

Projeto voltado para o aprendizado dos fundamentos do `django 2.x`.

## venv

Com o `python3-venv` instalado, criamos um ambiente python no diretório atual usando o comando:
```shell script
python3 -m venv [ambiente]
source [ambiente]/bin/activate
```


> importante: sempre utilizar ambientes ao desenvolver em python, garantindo sempre um sistema limpo e sem conflitos. 

## instalar django

Na pasta do projeto, instale o django.

```shell script
 python3 -m pip install django
```

> para conferir a instalação: 
 ```shell script
$ python

# dentro do console python
>>> import django
>>> django.VERSION
```

Se tudo foi instalado e configurado corretamente, será impresso na tela a versão do django.

## criar um projeto

Primeiramente devemos criar o projeto:

```shell script
django-admin startproject [projeto] .
```

## criando apps

Dentro de um projeto django podemos ter inúmeras apps. Para criar um app, na pagina do projeto:

```shell script
python manage.py startapp [app]
```

Após a criação, devemos registrá-lo em `/[projeto]/settings.py`.

## criando banco de dados

Com o banco de dados definido em `/[projeto]/settings.py` (sqlite3 por default), rodamos o comando:

```shell script
python manage.py migrate  
```

## rodando o servidor pela primeira vez

Após a configuração basica pronta, podemos rodar pela primeira vez a aplicação.

```shell script
python manage.py runserver
```

## criando um superuser

Para acessar o django-admin podemos usar o comando

```shell script
python manage.py createsuperuser
```


Finalmente a aplicação está pronta para para ser trabalhada

---

## trabalhando a app

Conceitos importantes e onde modificar.

## url

As urls do projeto, que irão ser mapeadas para as views devem ser adicionados ao arquivo `urls.py`. 

```python
from django.contrib import admin
from django.urls import path
from [projeto].views import [função ou classe]

urlpatterns = [
    path('admin/', admin.site.urls),
    path('[url]/', [função ou classe]),
]
```

### view

As urls que foram mapeadas no `import` e devem ser criados no arquivo `[app]/views.py`. As views podem retornar uma página ou um template. 

```python
# exemplo de página
from django.http import HttpResponse
import datetime

def home(request):
    now = datetime.datetime.now()
    html = "<html><body>It is now %s.</body></html>" % now
    return HttpResponse(html)
```

> retorna um html plano

Podemos usar também a função render, para retornar um template html.

```python
from django.shortcuts import render
import datetime

def home(request):
    now = datetime.datetime.now()
    html = "<html><body>It is now %s.</body></html>" % now
    return render(request, 'contas/home.html')
```

### templates

Devemos criar o diretório `[app]/templates/[app]/` e inserir arquivos HTML contendo os templates.

## models

Os dados são armazenados seguindo os models. Os models são classes extendidas de `models.Model`, que serão as tabelas, e os atributos são os campos a serem criados no banco de dados.

### criando o banco

Após definir o model, criamos o arquivo que irá gerar os comandos SQL e gerar a estrutura.
```shell script
python manage.py makemigrations
```

> o comando `makemigrations` verifica as alterações na pasta `models`  e gera um arquivo `migrations` dentro da pasta `migrations/`.

Após criado o arquivo de migração, criamos as tabelas no banco usando os comandos:
```shell script
python manage.py migrate
```

### testando a migração

Em `admin.py` adicionar as linhas:

```python

```