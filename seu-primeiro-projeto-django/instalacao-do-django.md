# Instalação do Django

### Ambiente virtual <a id="ambiente-virtual"></a>

Vamos fazer um virtualenv chamado `myvenv`. O formato geral desse comando é:

command-line\(terminal\)

```text
$ python3 -m venv myvenv
ou
$ python -m venv myvenv
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

Agora, execute:

`pip install -r requirements.txt` 

Assim vamos instalar o Django!!

command-line\(importante verificar se após o comando acima, o terminal fica como a tela abaixo\)

```text
(myvenv) ~$ pip install -r requirements.txt
Collecting Django~=2.2.4 (from -r requirements.txt (line 1))
  Downloading Django-2.2.4-py3-none-any.whl (7.1MB)
Installing collected packages: Django
Successfully installed Django-2.2.4
```

### Importante!

No terminal, rode o comando abaixo \(\*\*não esqueça de adicionar o ponto `.` no final!!

command-line\(terminal\)

```text
(myvenv) ~/djangoGirls$ django-admin startproject mysite .
```

> O ponto `.` é crucial por que ele diz para o script instalar o Django no diretório atual \(o ponto `.` é um atalho para referenciar este diretório\).
>
> **Observação:** Quando digitar o comando acima, lembre-se de digitar apenas a parte que começa em `django-admin`. A parte `(myvenv) ~/djangoGirls$` apresentada aqui é apenas um exemplo do que pode aparecer no seu terminal quando você digitar seus comandos.

É isto! Você agora \(finalmente\) está pronta para criar uma aplicação Django!

### OBSERVAÇÃO:

Se o arquivo `main.py` ainda esta dentro do diretório\(pasta\) `djangoGirls`, ele pode ser deletado neste momento. Pode clicar com o botão direito em cima do arquivo e selecionar a opção delete

