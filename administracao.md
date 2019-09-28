# Administração

Para adicionar, editar e remover postagens que nós criamos usaremos o Django admin. Vamos abrir o arquivo blog/admin.py e substituir seu conteúdo por:

```text
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

Após alterar, salve o arquivo \(“Save file”\)!

Como você pode ver, nós importamos \(incluímos\) o modelo Post definido no capítulo anterior. Para tornar nosso modelo visível na página de administração, nós precisamos registrá-lo com: `admin.site.register(Post)`.

OK, hora de olhar para o nosso modelo de Post. Lembre-se de acessar o ícone na lateral esquerda da tela de novo. Vá no navegador e adicione na URL o /admin. No nosso exemplo vai ficar [https://b6sdo2j4.apps.lair.io/admin](https://b6sdo2j4.apps.lair.io/admin) Você verá uma página de login assim:

![P&#xE1;gina de login](https://tutorial.djangogirls.org/pt/django_admin/images/login_page2.png)

Para fazer login, você precisa criar um _superusuário \(superuser\)_ - uma conta de usuário que pode controlar tudo no site. Volte à linha de comando, digite:

`python manage.py createsuperuser` 

e aperte Enter.

Para fazer login você precisa criar um superuser - um usuário que possui controle sobre tudo do site. Volte para o terminal e digite:

`python3 manage.py createsuperuser`

pressione enter 

digite seu nome de usuário \(caixa baixa, sem espaço\)

endereço de e-mail e password 

Não se preocupe que você não pode ver a senha que você está digitando - é assim que deve ser. Só digitá-la e pressione 'Enter' para continuar. A saída deve parecer com essa \(onde Username e Email devem ser os seus\):

```text
…@djangoGirls:/mnt/project$ python3 manage.py createsuperuser
Username (leave blank to use 'www-data'): admin
Email address: admin@admin.com
Password: Afropython123
Password (again): Afropython123
Superuser created successfully.
```

Volte para a o navegador e faça login com as credenciais de superuser que você escolheu, você deve visualizar o painel de controle do Django admin.

![Django Admin](https://tutorial.djangogirls.org/pt/django_admin/images/django_admin3.png)

Vá para as postagens e experimente um pouco com elas. Adicione cinco ou seis postagens. Não se preocupe com o conteúdo - você pode copiar e colar algum texto deste tutorial para o conteúdo para economizar tempo :\).

Certifique-se que pelo menos duas ou três postagens \(mas não todas\) tenham a data de publicação definida. Isso será útil depois.

![](.gitbook/assets/image%20%282%29.png)

Se você quiser saber mais sobre o Django admin, você deve conferir a documentação do Django: [https://docs.djangoproject.com/en/1.8/ref/contrib/admin/](https://docs.djangoproject.com/en/1.8/ref/contrib/admin/)

Este é provavelmente um bom momento para tomar um café \(ou chocolate\) ou algo para comer para repor as energias. Você criou seu primeiro modelo de Django - você merece um pouco de descanso!

