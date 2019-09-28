---
description: >-
  Parte deste capítulo é baseada nos tutoriais da Geek Girls Carrots
  (https://github.com/ggcarrots/django-carrots).Parte deste capítulo é baseado
  no django-marcador tutorial licenciado sobre Creative
---

# Seu primeiro projeto Django!

Nós vamos criar um blog simples!

O primeiro passo é iniciar um novo projeto Django. Basicamente, isso significa que devemos rodar alguns scripts providos pelo Django que vão criar um esqueleto de projeto Django para nós. O resultado é um conjunto de diretórios e arquivos que nós iremos utilizar e modificar mais tarde.

Os nomes de alguns arquivos e diretórios são muito importantes para o Django. Você não deve renomear os arquivos que estamos prestes a criar. Mover para um lugar diferente também não é uma boa idéia. O Django precisa manter uma certa estrutura para conseguir encontrar algumas coisas importantes.

> Lembre-se de rodar tudo no virtualenv. Se você não vê um prefixo `(myvenv)` em seu console, é necessário ativar o virtualenv. Nós explicamos como fazer isso no capítulo **Instalação do Django** na parte **Ambiente Virtual**. Digitar 
>
> > ```text
> > . myvenv/bin/activate
> > ```
>
>  no prompt de comando na pasta 'djangoGirls' no codenvy.

`django-admin` é um script que criará os diretórios e arquivos para você. Agora, você deve ter uma estrutura de diretório parecida com isso:

```text
djangogirls
├───manage.py
├───mysite
│        settings.py
│        urls.py
│        wsgi.py
│        __init__.py
└───requirements.txt
```

> **Observação:** em sua estrutura de diretórios, você também verá o o diretório do virtualenv, `venv`, que criamos antes.

`manage.py` é um script que ajuda com a gestão do site. Com ele, podemos iniciar um servidor de web no nosso computador sem instalar nada, entre outras coisas.

O arquivo `settings.py` contém a configuração do seu site.

Lembra de quando falamos sobre um carteiro verificando onde entregar uma carta? O arquivo `urls.py` contém uma lista dos padrões usados por `urlresolver`.

Vamos ignorar os outros arquivos por enquanto pois não vamos modificá-los. Só precisamos lembrar de não excluí-los por acidentalmente!

### Mudando as configurações <a id="mudando-as-configura&#xE7;&#xF5;es"></a>

Vamos fazer algumas alterações no `mysite/settings.py`. Abra o arquivo no codenvy.

**Observação:** Lembre-se de que o `settings.py` é um arquivo comum, como qualquer outro. Você pode abri-lo de dentro do editor de código usando as ações de menu "Arquivo-&gt; Abrir". Assim, você deve encontrá-lo na janela usual para selecionar arquivos e abri-lo. Ou então, é possível abrir o arquivo navegando até o diretório do djangogirls e abrindo o arquivo com o botão direito. Uma vez clicado, selecione o seu editor de código preferido da lista. Selecionar o editor apropriado é importante uma vez que você pode ter outros programas instalados que podem abrir o arquivo, mas não editá-lo.

Para começar, seria bom ter a hora correta no nosso site. Para isto, você configurar o fuso horário correto de onde está. Se você estiver no Brasil, é bem provável que o fuso horário seja `America/Sao_Paulo` \(aqui conhecido como horário de Brasília\). Caso queira saber mais, vá para [Wikipedia's list of time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) e copie e cole o fuso horário correspondende à sua localização.

Em `settings.py`, localize a linha que contém `TIME_ZONE` e modifique para escolher seu próprio fuso horário:

mysite/settings.py

```text
TIME_ZONE = 'America/Sao_Paulo'
```

Um código de idioma se refere à língua, por exemplo, `en` para inglês ou `pt` para português e o código do país, por exemplo, `br` para Brasil ou `pt` para a Portugal. Já que o inglês provavelmente não é sua língua nativa, você pode pode adicionar um novo código de país para deixar os botões padrão e notificações de Django em seu idioma. Assim, você teria por exemplo um botão "Cancel" traduzido para a língua da sua escolha \(ex: "Cancelar" em português\). O [Django vem com um monte de traduções já preparadas](https://docs.djangoproject.com/en/2.0/ref/settings/#language-code).

Se você quiser um idioma diferente do inglês, especifique o código de idioma alterando a seguinte linha:

mysite/settings.py

```text
LANGUAGE_CODE = 'pt-BR'
```

Também precisamos adicionar o caminho para os arquivos estáticos. \(Discutiremos tudo sobre arquivos estáticos e CSS mais adiante no tutorial.\) Vá até o _final_ do arquivo e, logo abaixo da linha com `STATIC_URL`, adicione uma nova variável chamada `STATIC_ROOT`:

mysite/settings.py

```text
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

Quando `DEBUG` for `True` e `ALLOWED_HOSTS` estiver vazia, o domínio do site será validado como `['localhost', '127.0.0.1', '[::1]']`. Isso não corresponderá ao nosso domínio no Codenvy quando implantarmos a nossa aplicação, então vamos mudamos a seguinte configuração:

mysite/settings.py

```text
ALLOWED_HOSTS = ['127.0.0.1', '.codenvy.io']
```

### Configurando um banco de dados <a id="configurando-um-banco-de-dados"></a>

Existem vários software de banco de dados diferentes que podem armazenar dados para o seu site. Nós vamos usar o padrão do Django, o `sqlite3`.

Isto já está configurado nesta parte do seu arquivo `mysite/settings.py`:

mysite/settings.py

```text
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

Para criar um banco de dados para o nosso blog, vamos executar o seguinte comando no console. 

Digite: 

```text
(myvenv) ~/djangogirls$ python manage.py migrate
```

 

precisamos estar no diretório que contém o arquivo `manage.py` `djangogirls`. Se isso der certo, você deve ver algo assim:

command-line

```text
(myvenv) ~/djangogirls$ python manage.py migrate
Operations to perform: 
  Apply all migrations: auth, admin, contenttypes, sessions
Running migrations: 
  Rendering model states... DONE
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK
```

Pronto! Hora de iniciar o servidor web e ver se nosso site está funcionando!

### Iniciando o servidor web <a id="iniciando-o-servidor-web"></a>

Você precisa estar no diretório que contém o arquivo `manage.py` \(o diretório `djangogirls`\). No console, nós podemos iniciar o servidor web executando o `python manage.py runserver`:

command-line

```text
 (myvenv) ~/djangogirls$ python manage.py runserver
```

Agora você precisa checar se o o seu site está funcionando!

Digite o comando abaixo: 

```text
(myvenv) ~/djangogirls$ python manage.py runserver 0.0.0.0:8080
```

se não funcionar, tente este outro comando:

```text
(myvenv) ~/djangogirls$ python manage.py runserver 0:8080
```

Você precisa estar no diretório que contém o arquivo manage.py \(o diretório djangogirls\). No console, nós podemos iniciar o servidor web executando o python manage.py runserver: command-line python manage.py runserver 0:8080

Seu site está no ar! Mas… como fazer para acessá-lo?

Precisamos buscar a url do Codenvy. Para isso, clique em Workspaces, no lado esquerdo da tela:

![](https://lh6.googleusercontent.com/3gax6B1eDEj8IphWFEBexXSl8UqW7oH4wMWfFYXwtrszrkPkS6u6lffGj_GbuCMmv3UfPP7am6GDJbYB_e5H2PLlmlBygfBo7NFyAItJuftXfjrneO6mxbjeEuRjgl0nwTetWdZC)



![](https://lh3.googleusercontent.com/v7SN2m5DLQ_xmC8E_ztKcALb6ZVJ5bGFuGsFHatJTcr9Bqyewgy0FybDX66c-nfYaniN-ohNvbPqAvpPdPGoqaKUFqtO8_nvz9-d7UFyP6pCLgKSNfDwt9fHbhLOR94IHqolGRQo)

![](https://lh5.googleusercontent.com/9K94LilxQE_SeYCsSzof4-u7lwApKGLN_67ITkWH8mklbVPWYNa-GNeof3ULfhGeoFNlZmbkJ8z1ngkahFSeCaw--t6wJd6Y2U511DcfeMxokkkMrf9PD7Xpkn4Uk9nYCF9UW7Kg)

Agora, procure na lista o servidor que está na porta 8080. Copie o endereço que está ao lado e cole em uma nova aba do navegador, vai ser tipo o exemplo abaixo:

```text
http://node11.codenvy.io:54664/
```

Se funcionou corretamente, então uma aba do navegador padrão do computador que esta utilizando vai abrir uma tela como a imagem abaixo.

![Instala&#xE7;&#xE3;o funcionou!](https://tutorial.djangogirls.org/pt/django_start_project/images/install_worked.png)

Parabéns! Você criou seu primeiro site e o executou usando um servidor web! Não é impressionante?

Note que a janela de comando só pode rodar uma coisa de cada vez, e a janela de comando que você abriu anteriormente já está rodando o servidor. Enquanto o servidor web estiver executando e esperando por solicitações de entrada, o terminal vai aceitar o novo testo mas não executará novos comandos.

> Nós revisamos como servidores web funcionam no capítulo **Como a Internet funciona**.

Para digitar comandos adicionais enquanto o servidor está rodando, abra uma nova janela de terminal e ative seu ambiente virtual, para revisar as instruções de como abrir uma segunda janela de terminal, veja [Introdução à linha de comando](https://tutorial.djangogirls.org/pt/intro_to_command_line/). Para interromper o seu servidor, volte para a janela onde ele está rodando e pressione CTRL+C -- botões Control e C juntos.

Pronta para o próximo passo? Está na hora de criar conteúdo!

