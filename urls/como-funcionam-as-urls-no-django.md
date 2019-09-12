# Como funcionam as URLs no Django?

Vamos abrir o arquivo `djangoGirls/urls.py`, ele deve ser alterado para ficar assim:

```text
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

Como você pode ver, o Django já colocou alguma coisa lá pra nós.

A URL do admin, que você visitou no capítulo anterior já está aqui:

```text
path('admin/', admin.site.urls),
```

Isso significa que para cada URL que começa com `admin/` o Django irá encontrar um correspondente modo de exibição. Neste caso nós estamos incluindo um monte de admin URLs para que isso não fique tudo embalado neste pequeno arquivo é também mais legível e mais limpo.

