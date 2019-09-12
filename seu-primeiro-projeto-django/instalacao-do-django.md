---
description: >-
  Observação: Se você está usando um Chromebook, pule este capítulo e
  certifique-se de seguir as instruções para Configuração do
  Chromebook.Observação: Se você já seguiu o passo a passo da instalação,
---

# Instalação do Django

### Ambiente virtual <a id="ambiente-virtual"></a>

Antes de instalar o Django, vamos instalar uma ferramenta muito útil para ajudar a manter o ambiente de trabalho no nosso computador organizado. Você pode pular esse passo, mas ele é altamente recomendado. Começar com a melhor instalação possível poupará você de muito trabalho no futuro!

Vamos criar um **ambiente virtual** \(também chamado um _virtualenv_\). O virtualenv isolará seu código Python/Django em um ambiente organizado por projetos. Isso significa que as alterações que você fizer em um website não afetarão os outros projetos que você estiver desenvolvendo ao mesmo tempo. Legal, né?

Tudo o que você precisa fazer é encontrar o diretório em que você quer criar o `virtualenv`; seu diretório será a pasta 'djangoGirls' que você criou na plataforma codenvy. 

Para este tutorial, usaremos um novo diretório `djangogirls` no seu diretório home:

command-line

```text
$ mkdir djangogirls // use este comando somente se você não tem esta pasta criada!
$ cd djangogirls
```

Vamos fazer um virtualenv chamado `myvenv`. O formato geral desse comando é:

command-line

```text
$ python3 -m venv myvenv
```

### Trabalhando com o virtualenv <a id="trabalhando-com-o-virtualenv"></a>

O comando acima criará um diretório chamado `myvenv` \(ou qualquer que seja o nome que você escolheu\) que contém o nosso ambiente virtual \(basicamente um conjunto de diretórios e arquivos\).

Inicie o seu ambiente virtual executando:

command-line

```text
$ source myvenv/bin/activate
```

Lembre-se de substituir `myvenv` pelo nome que você escolheu para o `virtualenv`!

> **Observação:** às vezes `source` pode não estar disponível. Nesses casos, tente fazer isso:
>
> command-line
>
> ```text
> $ . myvenv/bin/activate
> ```



Você vai saber que tem um `virtualenv` funcionando quando vir que a linha de comando no seu console tem o prefixo `(myvenv)`.

Ao trabalhar em de um ambiente virtual, o comando `python` irá automaticamente se referir à versão correta para que você possa digitar `python` em vez de `python3`.

Pronto, já temos todas as dependências importantes no lugar. Finalmente podemos instalar o Django!

### Instalando o Django <a id="instalando-o-django"></a>

Agora que você tem seu `virtualenv` ativo, pode instalar o Django\(Siga corretamente estes passos!!\).

Antes de fazer isto, devemos garantir que temos instalada a última versão do `pip`, que é o software que usamos para instalar o Django:

command-line

```text
(myvenv) ~$ python -m pip install --upgrade pip
```

#### Instalando pacotes com requisitos <a id="instalando-pacotes-com-requisitos"></a>

O arquivo "requirements.txt" guarda as dependências que serão instaladas utilizando o `pip install`:

Primeiro, crie um arquivo `requirements.txt` dentro da sua pasta `djangogirls/` usando o adicionar arquivo da plataforma codenvy . Para fazer isso, abra um novo arquivo no codenvy e salve-o como `requirements.txt` na pasta `djangogirls`. O seu diretório vai parecer com isso:

```text
djangogirls
└───requirements.txt
```

E adicione o seguinte texto ao arquivo `djangogirls/requirements.txt`:

djangogirls/requirements.txt

```text
Django~=2.2.4
```

Agora, execute `pip install -r requirements.txt` para instalar o Django.

command-line

```text
(myvenv) ~$ pip install -r requirements.txt
Collecting Django~=2.2.4 (from -r requirements.txt (line 1))
  Downloading Django-2.2.4-py3-none-any.whl (7.1MB)
Installing collected packages: Django
Successfully installed Django-2.2.4
```

É isto! Você agora \(finalmente\) está pronta para criar uma aplicação Django!

