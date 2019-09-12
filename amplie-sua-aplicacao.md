# Amplie sua aplicação

Já concluímos todos os passos necessários para a criação do nosso site: sabemos como criar um modelo, uma url, uma view e um template. Também sabemos como melhorar a aparência do nosso website.

Hora de praticar!

A primeira coisa que precisamos no nosso blog é, obviamente, uma página para mostrar uma postagem, certo?

Já temos um modelo de `Post`, então não precisamos adicionar nada ao `models.py`.

## Criar um link de template para um "detalhe" da postagem

Vamos começar com a adição de um link dentro do arquivo `blog/templates/blog/post_list.html`. Neste momento ele deve se parecer com: blog/templates/blog/post\_list.html

```markup
{% extends 'blog/base.html' %}

{% block content %}
    {% for post in posts %}
        <div class="post">
            <div class="date">
                {{ post.published_date }}
            </div>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaksbr }}</p>
        </div>
    {% endfor %}
{% endblock %}
```

blog/templates/blog/post\_list.html

```markup
<h1><a href="{% url 'post_detail' pk=post.pk %}">{{ post.title }}</a></h1>
```

Tempo para explicar o misterioso \`

`. Como você pode suspeitar, a notação`

\` significa que estamos usando as tags de template do Django. Desta vez, vamos usar uma que vai criar uma URL para nós!

`blog.views.post_detail` é um caminho para uma _view_ `post_detail` que queremos criar. Preste atenção: `blog` é o nome da sua aplicação \(o diretório `blog`\), `views` vem do nome do arquivo `views.py` e, a última parte - `post_detail` - é o nome da _view_.

Agora quando formos para sua página inicial, teremos um erro \(como esperado, já que não temos uma URL ou uma _view_ para `post_detail`\). Vai se parecer com isso:

![erro NoReverseMatch](https://tutorial.djangogirls.org/pt/extend_your_application/images/no_reverse_match2.png)

## Criando a URL para detalhe da postagem <a id="criando-a-url-para-detalhe-da-postagem"></a>

Vamos criar a URL em `urls.py` para a nossa _view_ `post_detail`!

Nós queremos que nosso primeiro detalhe de postagem seja exibido através dessa **URL**: http://&lt;&gt;/post/1/

Vamos criar uma URL no arquivo `blog/urls.py` para direcionar o Django para uma _view_ de nome `post_detail`, que irá exibir uma postagem de blog completa. Adicione a linha `path(r'^post/(?P<pk>\d+)/$', views.post_detail, name='post_detail'),` ao arquivo `blog/urls.py`. O arquivo deve ficar dessa forma:

blog/urls.py

```text
from django.urls import pathfrom blog import views​urlpatterns = [    path('', views.post_list),    path(r'^post/(?P<pk>[0-9]+)/$', views.post_detail, name='post_detail')]
```

O trecho `^post/(?P<pk>\d+)/$` parece assustador, mas não se preocupe – nós iremos explicar ele para você:

* ele começa com `^` novamente - "o início".
  * `post/` apenas significa que após o início, a URL deve ter a palavra **post** e um **/**. Até aqui, tudo bem.
  * `(?P<pk>\d+)` - essa parte é mais complicada. Isso significa que o Django vai pegar tudo que você colocar aqui e transferir para uma view através de uma variável chamada `pk`. `\d` também nos diz que só pode ser um número, não uma letra \(tudo entre 0 e 9\). `+` significa que precisa existir um ou mais dígitos. Então, algo como `http://<<sua_url>>/post//`, não é válido, mas `http://<<sua_url>>/post/1234567890/` é perfeitamente ok!
  * `/` - então precisamos de um **/** outra vez.
  * `$` - "o fim"!

Isso significa que, se você digitar `http://<<sua_url>>/post/5/` em seu navegador, Django vai entender que você está procurando uma _view_ chamada `post_detail` e transferir a informação de que `pk` é igual a `5` para aquela _view_.

`pk` é uma abreviação para `primary key` \(chave primária\). Esse é o nome geralmente usado nos projetos feitos em Django. Mas você pode dar o nome que quiser às variáveis \(lembre-se: minúsculas e `_` ao invés de espaços em branco!\). Por exemplo em vez de `(?P<pk>\d+)` podemos ter uma variável `post_id`, então esta parte ficaria como: `(?P<post_id>\d+)`.

OK, nós adicionamos um novo padrão de URL ao `blog/urls.py`! Vamos atualizar a página: `http://<<sua_url>>` Boom! O servidor parou de funcionar novamente. Dê uma olhada no console – como esperado, temos outro erro!

Você se lembra qual é o próximo passo? Claro: adicionar uma view!

## Adicionando a view de detalhe da postagem <a id="adicionando-a-view-de-detalhe-da-postagem"></a>

Desta vez a nossa _view_ recebe um parâmetro extra, `pk`. Nossa _view_ precisa pegá-la, certo? Então vamos definir nossa função como `def post_detail (request, pk):`. Observe que precisamos usar exatamente o mesmo nome que especificamos em urls \(`pk`\). Omitir essa variável é errado e resultará em um erro!

Agora queremos receber apenas um post do blog. Para isso podemos usar `querysets` como este:

blog/views.py

```text
def post_detail(request, pk):    Post.objects.get(pk=pk)
```

Mas este código tem um problema. Se não houver nenhum `Post` com a `chave primária` \(`pk`\) fornecida teremos um erro horroroso!

![erro NoReverseMatch](https://tutorial.djangogirls.org/pt/extend_your_application/images/no_reverse_match2.png)

Não queremos isso! Mas, claro, o Django vem com algo que vai lidar com isso para nós: `get_object_or_404`. Caso não haja nenhum `Post` com o `pk` informado, ele exibirá uma página muito mais agradável \(chamada `Page Not Found 404` - página não encontrada\).

![](.gitbook/assets/image%20%281%29.png)

A boa notícia é que você realmente pode criar sua própria página de `Page not found` e torná-la tão bonita quanto você quiser. Mas isso não é super importante agora, então nós vamos pular essa parte.

Ok, hora de adicionar uma _view_ ao nosso arquivo `views.py`!

Devemos abrir `blog/views.py` e adicionar o seguinte código perto das outras linha com `from`:

blog/views.py

```text
from django.shortcuts import render, get_object_or_404
```

E no final do arquivo, adicionaremos a nossa _view_:

blog/views.py

```text
def post_detail(request, pk):
    post = get_object_or_404(Post, pk=pk)
    return render(request, 'blog/post_detail.html', {'post': post})
```

Sim. Está na hora de atualizar sua página inicial.

![View da lista de posts](https://tutorial.djangogirls.org/pt/extend_your_application/images/post_list2.png)

Funcionou! Mas o que acontece quando você clica em um link no título do post do blog?

![erro TemplateDoesNotExist](https://tutorial.djangogirls.org/pt/extend_your_application/images/template_does_not_exist2.png)

Ah não! Outro erro! Mas nós já sabemos como lidar com isso, não é? Precisamos adicionar um template!

## Criação de um template para o detalhe da postagem <a id="criacao-de-um-template-para-o-detalhe-da-postagem"></a>

Vamos criar um arquivo em `blog/templates/blog` chamado `post_detail.html`.

Será algo parecido com isto:

blog/templates/blog/post\_detail.html

```text
{% extends 'blog/base.html' %}​{% block content %}    <div class="post">        {% if post.published_date %}            <div class="date">                {{ post.published_date }}            </div>        {% endif %}        <h1>{{ post.title }}</h1>        <p>{{ post.text|linebreaksbr }}</p>    </div>{% endblock %}
```

Mais uma vez estamos estendendo `base.html`. No bloco `content` queremos exibir o `published_date` \(data de publicação\) da postagem \(se houver\), título e texto. Mas devemos discutir algumas coisas importantes, certo?

Ok, podemos atualizar nossa página e ver se o `TemplateDoesNotExist`já se foi.

![P&#xE1;gina de detalhes da postagem](https://tutorial.djangogirls.org/pt/extend_your_application/images/post_detail2.png)

Yay! Funciona!

## Hora do Deploy!  <a id="hora-do-deploy"></a>

_Somente se você criou uma conta no pythonanywhere!!_

Seria bom ver se seu site ainda estará trabalhando no PythonAnywhere, né? Vamos tentar fazer a implantação novamente.

command-line

```text
$ git status
$ git add --all .
$ git status
$ git commit -m "Added view and template for detailed blog post as well as CSS for the site."
$ git push
```

Agora, em um [console Bash do PythonAnywhere](https://www.pythonanywhere.com/consoles/):

PythonAnywhere command-line

```text
$ cd ~/<your-pythonanywhere-domain>.pythonanywhere.com
$ git pull
[...]
```

\(Lembre-se de substituir `<your-pythonanywhere-domain>` com o nome do seu subdomínio PythonAnywhere, sem os colchetes angulares, ou seja, sem &lt; e &gt;\).

