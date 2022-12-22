# Django com DRF

Tutorial para desenvolvimento de APIs REST usando o [Django](https://www.djangoproject.com/) com [DRF](https://www.django-rest-framework.org/) (Django Rest Framework).

# 1. Preparação do ambiente

A preparação do ambiente será feita apenas uma vez em cada computador. Ela consiste em instalar e configurar o **VS Code**, o **PDM** e o **Python**.

**1.1 VS Code**

**1.1 Instalação do VS Code**

Caso não tenha o **VS Code** instalado, instale-o seguindo as instruções [deste link](https://code.visualstudio.com/download).

**1.2 Instalação de extensões no VS Code**

Instale as extensoẽs do **VS Code** de sua preferência. Você pode instalar as extensões clicando no ícone de extensões no canto esquerdo da tela do **VS Code** e pesquisando pelo nome da extensão.

-   Eu recomendo as seguintes:
    -   Better TOML (Syntaxe Destacada para TOML)
    -   ESLint (JavaScript)
    -   Intellicode (Desenvolvimento Inteligente)
    -   isort (Organização de imports)
    -   Material Icon Theme (Temas de ícones)
    -   Peacock (Personalização de cores)
    -   Portuguese (Brazil) Language Pack for Visual Studio Code (Tradução para Português da interface do VS Code)
    -   Prettier (Formatação de código)
    -   Python (Uhaa!)
    -   RapidAPI Client (Teste de APIs)
    -   SqLite Viewer (Visualização de bancos de dados SQLite)
    -   TypeScript Vue Plugin (Desenvolvimento de aplicações Vue.js)
    -   Vue Language Features (Desenvolvimento de aplicações Vue.js)

Você pode configurar a sincronização das extensões entre os computadores. Para isso, você precisa fazer login com a conta do **GitHub** ou da **Microsoft** no VS Code. Para isso, clique no ícone de engrenagem no canto inferior esquerdo da tela do VS Code e clique em `Ativar a Sincronização de Configurações`.

**1.2 Instalação do PDM**

As instruções a seguir são para o **Linux Manjaro**. Se você estiver usando outra distribuição ou quiser mais informações, consulte a documentação do [PDM](https://pdm.fming.dev/latest/).

-   Abra um terminal:

    `Ctrl + Alt + T`

-   Verifique se o **PDM** está instalado:

```shell
pdm -V
```

-   Se a versão for inferior a 2, instale a versão mais recente:

```shell
curl -sSL https://raw.githubusercontent.com/pdm-project/pdm/main/install-pdm.py | python3 -
```

**1.2.1 Configuração do auto preenchimento do PDM**

Ative o **auto preenchimento** do **PDM**, conforme o seu shell:

-   Para o **bash**:

```shell
pdm completions bash >> ~/.bash_completion
```

-   Para o **zsh**:

```shell
pdm completions zsh >> ~/.zshrc
```

-   Para o **Oh My Zsh**:

```shell
mkdir $ZSH_CUSTOM/plugins/pdm
pdm completion zsh > $ZSH_CUSTOM/plugins/pdm/_pdm
```

No caso do **Oh My Zsh**, você precisa adicionar `pdm` à lista de plugins no arquivo `~/.zshrc`.

**1.2.2 Habilitar o PEP 582 no PDM**

```shell
pdm --pep582 >> ~/.zshrc #zsh
pdm --pep582 >> ~/.bash_profile #bash
```

**1.2.3 Instalação de plugins do PDM**

-   Instale o plugin **pdm-vscode**, que permite a integração do **PDM** com o **VS Code**:

```shell
pdm add pdm-vscode
```

-   Instale o plugin pdm-autoexport, que atualiza automaticamente o arquivo `requirements.txt`, cada vez que você instalar um pacote:

```shell
pdm add pdm-autoexport
```

**1.3 Instalação do Python**

-   Verifique se o **python** está instalado:

```shell
python --version
python3 --version
```

# 2. Criação do projeto

**2.1 Criação da pasta do projeto**

-   Abra o navegador de arquivos:

    `Windows + E`

-   Entre na pasta **Documentos** ou crie uma pasta **projetos**.
-   Crie uma pasta chamada `livraria` (ou outro nome de sua preferência) para o seu projeto.
-   **IMPORTANTE**:
    -   Não trabalhe na `Área de Trabalho` ou na pasta `Downloads`.
    -   Certifique-se de que **nenhuma pasta** no caminho tenha **espaços** ou **acentos** (**se você não fizer isso, terá que recriar todo o projeto**).
-   Dentro dessa pasta, abra um terminal:

    _Botao direito do mouse -> Abrir terminal aqui_

**2.2 Criação do projeto no PDM**

-   Crie o projeto com o **PDM**:

```shell
pdm init
```

-   Você passará por uma tela semelhante a essa:

```shell
Creating a pyproject.toml for PDM...
Please enter the Python interpreter to use
1. /usr/bin/python (3.10)
2. /usr/bin/python3.10 (3.10)
3. /home/marco/.local/share/pdm/venv/bin/python (3.10)
Please select (0):
Using Python interpreter: /usr/bin/python (3.10)
Would you like to create a virtualenv with /usr/bin/python? [y/n] (y): n
You are using the PEP 582 mode, no virtualenv is created.
For more info, please visit https://peps.python.org/pep-0582/
Is the project a library that will be uploaded to PyPI [y/n] (n): n
License(SPDX name) (MIT):
Author name (Marco André Mendes):
Author email (marcoandre@gmail.com):
Python requires('*' to allow any) (>=3.10):
Changes are written to pyproject.toml.
```

-   Entre na pasta do projeto:

```shell
cd livraria
```

-   Verifique se o **PDM** criou o arquivo `pyproject.toml`:

```shell
ls -l pyproject.toml
```

**2.3 Abrindo o projeto no VS Code**

-   Abra o projeto no VS Code:

```shell
code .
```

Você pode abrir o projeto no VS Code de duas formas:

-   Digitando o comando `code .` no terminal.
-   Pelo gereciador de arquivos, clicando com o botão direito do mouse na pasta do projeto e selecionando a opção **Abrir com o VS Code**.
-   Clicando no botão **Abrir pasta** e selecionando a pasta do projeto.

**IMPORTANTE:**

-   Sempre abra a **pasta raiz do projeto** no VS Code (repita em voz alta: _"**Nunca** abra um **arquivo**, **sempre** abra a **pasta**."_).\*\*
-   O VS Code precisa dessa informação de qual é a pasta raiz do projeto para funcionar corretamente.

**2.4 Instalação do Django**

-   Instale o **Django** no seu projeto:

```shell
pdm add django
```

-   Verifique se o arquivo `pdm.lock` foi criado:

```shell
ls -l pdm.lock
```

-   Verifique a versão do **Django** instalado:

```shell
pdm run django-admin --version
```

**Criação do projeto no Django**

Um projeto no **Django** é uma pasta com um conjunto de arquivos e pastas que contém o código do seu site.

-   Crie o projeto no **Django**:

```shell
pdm run django-admin startproject config .
```

**IMPORTANTE**: o ponto no final é importante. Ele indica que o projeto será criado na pasta atual.

O projeto criado ficará assim:

```
.
├── .vscode
│   ├── settings.json
├── config
│   ├── asgi.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
├── pdm.lock
├── pyproject.toml
└── requirements.txt
```

**Abra um terminal no VS Code**

Ctrl + Shift + `

**Rodando o servidor de desenvolvimento**

-   Para executar o projeto, digite no terminal:

```shell
pdm run python manage.py runserver
```

-   Verifique se o projeto está rodando:

    -   Página inicial: http://localhost:8000
    -   `Admin`: http://localhost:8000/admin

-   Ao rodar o projeto pela primeira vez, o arquivo `db.sqlite3` é criado.
-   Também aparecem mensagens de erro importantes.
-   Abra o arquivo `db.sqlite3` dentro do **VS Code**.
-   Verifique que ele ainda não possui nenhuma tabela.

-   Vamos abrir cada um desses arquivos e verificar para que eles servem, principalmente os seguintes:

    -   `manage.py`: é o arquivo que você usa para executar comandos do **Django**.
    -   `settings.py`: é o arquivo de configuração do projeto.
    -   `urls.py`: é o arquivo de configuração das rotas do projeto.
    -   `db.sqlite3`: é o arquivo de banco de dados do projeto.

**Executando o servidor**

Desse ponto em diante, abra um outro terminal lado a lado no **VS Code**, mantendo sempre o django em execução (`runserver`) no outro terminal.

Se precisar parar a execução do projeto, aperte `Control+C` e depois o execute novamente.

**Criando a base de dados inicial**

-   Para resolver o erro informado no momento de rodar o projeto, execute o seguinte comando:

```shell
pdm run python manage.py migrate
```

Verifique se o projeto continua rodando e se o [Admin](http://localhost:8000) está em execução.

**Criando o superusuário**

-   Crie o super usuário para poder fazer o login:

```shell
pdm run python manage.py createsuperuser
```

-   Agora sim, seu projeto está rodando e você consegue entrar no `Admin`:

-   Crie mais 2 usuários de teste.
-   Entre no arquivo de banco de dados (`db.sqlite3`), e verifique se os registros foram criados.

**Exercício**

-   Apague o projeto e crie novamente, seguindo as instruções acima.
-   Verifique se o projeto está rodando e se o `Admin` está em execução.
-   Observe que configurações precisam ser feitas novamente e quais não foram mais necessárias.

# 3. Criação de uma aplicação

Uma aplicação no **Django** é um conjunto de arquivos e pastas que contém o código de uma funcionalidade específica do seu site.

**Criando uma aplicação**

-   Para criar uma aplicação, execute o seguinte comando:

```shell
pdm run python manage.py startapp livraria
```

-   Acrescente a aplicação `livraria` na seção `INSTALLED_APPS` do arquivo `settings.py` do seu projeto.

```python
INSTALLED_APPS = [
    ...
    "livraria",
]
```

Após criar a aplicação, sua pasta deve parecer com isso:

```
.
├── livraria
│   ├── admin.py
│   ├── apps.py
│   ├── __init__.py
│   ├── migrations
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── db.sqlite3
├── config
│   ├── asgi.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
├── pdm.lock
├── pyproject.toml
└── requirements.txt
```

Dentro da pasta `livraria` foram criados alguns arquivos, mas os mais importantes são:

-   `admin.py`: é o arquivo de configuração do `Admin` da aplicação.
-   `models.py`: é o arquivo de configuração dos modelos da aplicação.
-   `views.py`: é o arquivo de configuração das `views` da aplicação.
-   `migrations`: é a pasta de migrações da aplicação.

Posteriormente, iremos modificar esses arquivos, bem como incluir alguns arquivos novos.

**Resumo**

Nesse ponto, temos:

-   O projeto no `PDM` criado;
-   O projeto `config` criado;
-   A aplicação `livraria` criada e instalada no projeto.

**Criação do primeiro modelo de dados**

Um modelo (`model`) no **Django** é uma classe que representa uma tabela no banco de dados. Cada atributo (variável) dessa classe representa um campo da tabela.

Para maiores informações consulte a [documentação](https://docs.djangoproject.com/en/4.0/topics/db/models/) do **Django** sobre `models`.

-   Vamos criar o modelo de dados `Categoria`:

```python
from django.db import models

class Categoria(models.Model):
    descricao = models.CharField(max_length=100)
```

Nesse código, você:

-   Importou o pacote necessário para criar a `model`;
-   Criou a classe `Categoria`;
-   Incluiu o campo `descricao`.

**Efetivando a criação da tabela**

Precisamos agora efetivar a criação da tabela no banco de dados.

-   Abra um novo terminal, deixando o terminal antigo executando o servidor do projeto.

-   Crie as migrações:

```shell
pdm run python manage.py makemigrations
```

-   Execute as migrações:

```shell
pdm run python manage.py migrate
```

-   Acesse o arquivo do banco de dados e verifique se a tabela `livraria_categoria` foi criada.
-   Acesse o [Admin](http://localhost:8000) do projeto e verifique se a nova tabela aparece lá.

**Inclusão no Admin**

A tabela ainda não apareceu, certo? Isso acontece poque ainda não incluímos a `model` no `Admin`.

-   Vamos incluir a `model` no `Admin`:

```python
from django.contrib import admin

from .models import Categoria

admin.site.register(Categoria)
```

Acesse novamente o [Admin](http://localhost:8000) e inclua algumas editoras no banco de dados.

**Mudando a língua e time zone**

Encontre e edite as seguintes linhas no arquivo no arquivo `settings.py`:

```python
LANGUAGE_CODE = "pt-br"
TIME_ZONE = "America/Sao_Paulo"
```

Acesse novamente o [`Admin`](http://localhost:8000) e verifique que agora ele está em português.

**O campo `id`**

O campo `id` é criado automaticamente pelo **Django**. Ele é o identificador único de cada registro da tabela.

**O campo `__str__`**

O campo `__str__` é criado automaticamente pelo **Django**. Ele é o campo que será exibido no `Admin` e em outros lugares.

**Mudando a descrição dos registros criados**

-   Inclua algumas categorias no banco de dados.
-   Você perceberá que a descrição dos informações que você inclui está meio estranha.
-   Para resolver, isso, vamos fazer uma pequena modificação na `model Categoria`.

```python
...
    def __str__(self):
        return self.descricao
```

Volte ao [`Admin`](http://localhost:8000) verifique o que mudou na apresentação da model `Categoria`.

**Criação do modelo de dados Editora**

-   Vamos criar o modelo de dados `Editora`, no arquivo `models.py`:

```python
...

class Editora(models.Model):
    nome = models.CharField(max_length=100)
    site = models.URLField(null=True, blank=True)

    def __str__(self):
        return self.nome
```

O atributo `null=True` indica que o campo pode ser nulo. O atributo `blank=True` indica que o campo pode ser deixado em branco.

Não esqueça de que a cada criação de novas `models` é necessário:

-   Registrar a model no arquivo `admin.py`;
-   Fazer as migrações (`makemigrations`);
-   Efetivar as migrações (`migrate`);

Seu arquivo `admin.py` ficará assim:

```python
from django.contrib import admin

from core.models import Categoria, Editora

admin.site.register(Categoria)
admin.site.register(Editora)
```

Após fazer isso tudo, inclua algumas editoras na tabela e veja como ficou o seu banco de dados.

# 4. Criando um segundo projeto

Seguindo aquilo que você já aprendeu, crie um **novo projeto**:

-   Nome do projeto: **config**.
-   Nome da aplicação: **garagem**.
-   Crie os modelos conforme a definição abaixo.
-   Registre as models no `Admin`.
-   Inclua alguns registros no banco de dados.

```python
from django.db import models


class Marca(models.Model):
    nome = models.CharField(max_length=50)

    def __str__(self):
        return self.nome.upper()


class Categoria(models.Model):
    descricao = models.CharField(max_length=100)

    def __str__(self):
        return self.descricao
```

---

# 5. Colocando o projeto no GitHub

Antes de mais nada, seguem **3 regras** a serem consideradas ao seguir as instruções:

-   **Antes de clicar ou responder, leia atentamente as instruções.**
-   **Leia atentamente as instruções antes de clicar ou responder.**
-   **Nunca clique ou responda sem antes ler atentamente as instruções.**

As 3 regras falam a mesma coisa? Sim, você entendeu o recado. ;-)

**Configure o projeto git**

-   Se o computador estiver configurado com contas individuais, você precisará fazer isso apenas uma vez. Ainda assim, é bom verificar se está tudo certo.
-   Verifique se já não existe uma conta conectada ao **GitHub** no **VS Code**, clicando no ícone **Contas** na barra lateral esquerda. Deve ser o penúltimo ícone da baixo pra cima. Se houver, **desconecte primeiro**.
-   Inicialize o repositório **git**. Clique no ícone do **git** no painel lateral esquerdo. Deve ser o segundo ícone, de cima pra baixo. Opcionalmente, tecle (`Control+Shift+G`). Depois, clique no botão `Initialize repository`.
-   Se aparecer uma bolinha azul no ícone do git com um número, o repositório foi ativado. Esse número indica o número de arquivos que foram criados ou alterados.
-   Se aparecem muitos arquivos alterados (10 mil, por exemplo), é provável que exista um repositório **git** criado na pasta raiz do usuário. Apague esse repositório assim:

```shell
rm -Rf ~/.git
```

-   Recarregue a janela do **VS Code**:

```shell
Control + Shift + P + "Recarregar a Janela"
```

-   Verifique se o número mudou para algo mais razoável (em torno de 100 arquivos).

**Configure as variáveis do git**

-   Informe seu nome e email no git. Para isso, abra o terminal do VS Code e digite:

```shell
git config --global user.name "Seu Nome"
git config --global user.email "seuEmailNoGitHub@gmail.com"
```

-   Para verificar se as variáveis foram configuradas corretamente, digite:

```shell
git config -l
```

-   Se aparecer outro nome de usuário ou outras informações estranhas, remova o arquivo com as configurações globais do git:

```shell
rm ~/.gitconfig
```

Repita o processo de configuração de nome e email.

**Crie o arquivo `.gitignore`**

Vamos criar um arquivo chamado `.gitignore` na raiz do projeto. Esse arquivo serve para indicar quais arquivos não devem ser versionados (monitorados pelo **git**).

-   Vá no site [gitignore.io](https://gitignore.io/)
-   Escolha as opções `Python` e `Django`.
-   Clique em `Criar`.
-   Selecione todo o texto (`Control + A`) e copie (`Control + C`).
-   Crie um arquivo novo na raiz do projeto e dê o nome de `.gitignore`:

```shell
touch .gitignore
```

-   Cole o conteúdo copiado (`Control + V`).
-   Encontre as linhas que se referem a "`db.sqlite3`" e comente-as (`Control + /`).

**Faça a publicação**

-   Escreva uma descrição para o commit (`"commit Inicial"`, por exemplo.).
-   Tecle `Control+ENTER` para fazer o envio para o servidor do **GitHub**.
-   Leia atentamente as instruções relacionadas a autenticação no **GitHub** e criação do projeto.
-   Ao final, seu projeto será incluído no **GitHub** e você poderá visulizá-lo lá.

**Fazendo alterações no projeto e enviando novamente**

Vamos agora realizar algumas mudanças no projeto e enviá-lo novamente para o **GitHub**.

-   Abra o arquivo `models.py`:

```shell
Control + P + models.py
```

-   Selecione todo o texto (`Control + A`) e mande formatar o código:

```shell
Control + Shift + I
```

ou

```shell
Control + Shift + P + "Formatar o Documento"
```

-   Deve aparecer uma mensagem pedindo para instalar um **formatador de código** (`black`). Concorde com a instalação.
-   Após a instalação, execute o comando para formatar novamente. O arquivo deve ser formatado.
-   Faça a mesma coisa com o arquivo `admin.py`.
-   Altere outros arquivos. Por exemplo: apague os comentários iniciais dos arquivos `settings.py` e `urls.py`.
-   Nesse ponto, você já deve ter vários arquivos modificados.
-   Vá para a aba do **GitHub** no **VS Code** e coloque o nome do **commit** como sendo `Formatação dos arquivos do projeto`.
-   Confirme o **commit** teclando `Control+ENTER`.
-   Faça o envio (`push`), clicando no ícone de envio.
-   Vá no seu projeto no **GitHub**, atualize a página e verifique as modificações.

**IMPORTANTE: Escrevendo uma boa mensagem de commit**

-   Escreva uma mensagem de commit que descreva o que foi feito.
-   Dessa forma fica mais fácil identificar as mudanças sem precisar ver o código.
-   Não escreva mensagens como `Alteração 1`, `Alteração 2`, `Alteração 3`, etc.
-   Escreva mensagens como:
    -   `Adiciona o arquivo settings.py`
    -   `Adiciona o arquivo urls.py`
    -   `Adiciona o arquivo admin.py`

**Baixando novamente o projeto**

Agora que seu projeto está no **GitHub**, você pode baixá-lo onde quiser, seja na aula, em casa ou no trabalho, por exemplo. Vamos testar isso.

**A partir desse ponto, vamos repetir uma série de passos que já fizemos nas aulas anteriores. Em caso de dúvidas, volte nessas aulas para mais detalhes.**

-   Abra o terminal na pasta superior à pasta do projeto:

```shell
Control + Alt + T
```

-   Apague todo o projeto do seu computador (_isso mesmo, coragem_):

```shell
rm -rf livraria
```

-   Crie novamente uma pasta vazia para hospedá-lo:

```shell
mkdir livraria
```

-   Vá no projeto no **GitHub**, clique no botão **Code** e copie a URL dele. Deve ser algo no seguinte formato: `https://github.com/marrcandre/livraria.git`
-   Clone o projeto para a pasta atual:

```shell
git clone https://github.com/marrcandre/livraria.git #troque essa URL pela sua
```

-   Vá para a pasta do projeto:

```shell
cd livraria
```

-   Abra o projeto no **VS Code**:

```shell
code .
```

-   Instale as dependências do projeto e ative o ambiente virtual:

```shell
pdm install
```

-   Rode o servidor:

```shell
pdm run python manage.py runserver
```

-   Acesse o projeto no navegador:

    http://localhost:8000/

Pronto! Seu projeto está de volta no computador e rodando.

# 6. Criando os outros modelos de dados

**Colocando o projeto livraria no **GitHub\*\*\*\*

Agora que você conseguiu colocar o projeto `garagem` no **GitHub**, coloque também o projeto `livraria`.

**Criando o modelo de dados Autor**

-   Vamos criar o modelo de dados `Autor`, no arquivo `models.py`:

```python
...

class Autor(models.Model):
    nome = models.CharField(max_length=255)
    email = models.EmailField(null=True, blank=True)

    def __str__(self):
        return self.nome

    class Meta:
        verbose_name_plural = "Autores"
```

**Criando o modelo de dados Livro**

-   Vamos criar o modelo de dados `Livro`, no arquivo `models.py`:

```python

class Livro(models.Model):
    titulo = models.CharField(max_length=255)
    isbn = models.CharField(max_length=32, null=True, blank=True)
    quantidade = models.IntegerField(default=0)
    preco = models.DecimalField(max_digits=7, decimal_places=2, default=0)

    def __str__(self):
        return f"{self.titulo} ({self.quantidade})"
```

Antes de efetivarmos as alterações no banco de dados, vamos incluir duas chaves estrangeiras no modelo `Livro`.

**Incluindo chaves estrangeiras no modelo**

Nosso livro terá uma categoria e uma editora. Para isso, vamos incluir campos que serão chaves estrageiras, referenciando os modelos `Categoria` e `Editora`.

**Campo `categoria` no `Livro`**

-   Inclua a linha a seguir no modelo `Livro`, logo após o atributo `preco`:

```python
...
    categoria = models.ForeignKey(
        Categoria, on_delete=models.PROTECT, related_name="livros"
    )
...
```

-   Vamos entender cada parte:
    -   `models.ForeignKey`: define o campo como sendo uma chave estrangeira.
    -   `Categoria`: o model que será associado a esse campo.
    -   `on_delete=models.PROTECT`: impede de apagar uma _categoria_ que possua _livros_ associados.
    -   `related_name="livros"`: cria um atributo `livros` na classe `Categoria`, permitindo acessar todos os livros de uma categoria.

**Testando o atributo related_name**

No `Django Shell`, é possível testar o acesso a todos os livros de uma categoria usando algo parecido com isso:

-   Abrar o Django shell:

```shell
python manage.py shell
```

-   Acesse os livros da categoria com `id` 1:

```python
>>> from livraria.core.models import Categoria
>>> Categoria.objects.get(id=1).livros.all()
```

Mais na frente, aprenderemos a utilizar outros recursos do `Django Shell`.

**Campo `editora` no `Livro`**

-   De forma semelhante, vamos associar o livro a uma editora, incluindo logo em seguida à categoria, a seguinte linha:

```python
editora = models.ForeignKey(Editora, on_delete=models.PROTECT, related_name="livros")
```

-   Inclua os modelos criados no arquivo `admin.py`:

```python
from django.contrib import admin

from core.models import Autor, Categoria, Editora, Livro

admin.site.register(Autor)
admin.site.register(Categoria)
admin.site.register(Editora)
admin.site.register(Livro)
```

-   Prepare as migrações:

```shell
python manage.py makemigrations
```

-   Efetive as migrações:

```shell
python manage.py migrate
```

Feito isso, verifique se tudo funcionou.

-   Cadastre algumas categorias, editoras, autores e livros.
-   Note como os livros acessam as categorias e editoras já cadastradas.
-   Tente apagar uma editora ou categoria **com** livros associados.
-   Tente apagar uma editora ou categoria **sem** livros associados.

# 7. Criando uma API REST

**Instalação do DRF**

-   Instale o `djangorestframework`:

```shell
pdm add djangorestframework
```

-   Adicione o `rest_framework` no arquivo `settings.py`:

```python
INSTALLED_APPS = [
...
    "rest_framework",
    "core",
]
```

**Criação do serializer**

Um _serializer_ é um objeto que transforma um objeto do banco de dados em um objeto JSON.

-   Crie o arquivo `serializers.py` no diretório `livraria`:

```shell
touch core/serializers.py
```

-   Adicione o seguinte código no arquivo `serializers.py`:

```python
from rest_framework.serializers import ModelSerializer

from core.models import Categoria

class CategoriaSerializer(ModelSerializer):
    class Meta:
        model = Categoria
        fields = "__all__"
```

**Criação da view**

Uma _view_ é um objeto que recebe uma requisição HTTP e retorna uma resposta HTTP.

-   Crie a view `CategoriaViewSet` no arquivo `views.py`:

```python
from rest_framework.viewsets import ModelViewSet

from core.models import Categoria
from core.serializers import CategoriaSerializer

class CategoriaViewSet(ModelViewSet):
    queryset = Categoria.objects.all()
    serializer_class = CategoriaSerializer
```

**Criação das rotas(urls)**

As rotas são responsáveis por mapear as URLs para as views.

-   Para criar as rotas da `Categoria`, edite o arquivo `urls.py` na pasta `livraria`. Substitua o seu conteúdo por esse:

```python
from django.contrib import admin
from django.urls import include, path

from rest_framework.routers import DefaultRouter

from core.views import CategoriaViewSet

router = DefaultRouter()
router.register(r"categorias", CategoriaViewSet)

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include(router.urls)),
]
```

**Testando a API**

-   Para acessar a interface gerada pelo DRF, acesse:

    http://localhost:8000

Se tudo correu bem, você deve ver a interface do DRF.

-   Você pode acessar diretamente a rota da `Categoria`:
    http://localhost:8000/categorias/

Isso deve trazer todas as categorias do banco, no formato **JSON**.

-   Para acessar um único registro, use o seguinte formato:
    http://localhost:8000/categorias/1/

Nesse caso, `1` é o `id` do registro no banco de dados.

**Opções de manipulação do banco de dados**

As opções disponíveis para manipulação dos dados são:

-   **GET** para **listar** **todos** os registros: http://localhost:8000/categorias/
-   **GET** para **listar** **apenas 1** registro: http://localhost:8000/categorias/1/
-   **POST** (para **criar** um **novo** registro): http://localhost:8000/categorias/
-   **PUT** (para **alterar** um registro existente): http://localhost:8000/categorias/1/
-   **PATCH** (para **alterar parcialmente** um registro): http://localhost:8000/categorias/1/
-   **DELETE** (para **remover** um registro): http://localhost:8000/categorias/1/

**Outras ferramentas para testar a API**

A interface do DRF é funcional, porém simples e limitada. Algumas opções de ferramentas para o teste da API são:

-   [Insomnia](https://docs.insomnia.rest/insomnia/install)
-   [Postman](https://www.postman.com/downloads/)
-   [RapidAPI](https://marketplace.visualstudio.com/items?itemName=RapidAPI.vscode-rapidapi-client) (extensão do **VS Code**)

**Testando a API e as ferramentas**

Instale uma ou mais das ferramentas sugeridas.

-   Experimente as seguintes tarefas:
    -   Criar uma ou mais categorias;
    -   Listar todas as categorias;
    -   Alterar uma ou mais categorias, utilizando PUT e PATCH;
    -   Listar a categoria alterada;
    -   Remover uma categoria;
    -   Incluir outra categoria;
    -   Listar todas as categorias.

# 8. Continuando a criação da API REST

**Criação da API para a classe Editora**

Crie a API para a classe `Editora` seguindo os passos anteriores.

-   Os passos são:

    -   Criar o serializador em `serializers.py`
    -   Criar a viewset em `views.py`.
    -   Incluir a nova rota em `urls.py`

-   Os arquivos ficarão assim:

**`serializers.py`**

```python
from rest_framework.serializers import ModelSerializer

from core.models import Categoria, Editora

class CategoriaSerializer(ModelSerializer):
    class Meta:
        model = Categoria
        fields = "__all__"


class EditoraSerializer(ModelSerializer):
    class Meta:
        model = Editora
        fields = "__all__"
```

**`views.py`**

```python
from rest_framework.viewsets import ModelViewSet

from core.models import Categoria, Editora
from core.serializers import CategoriaSerializer, EditoraSerializer

class CategoriaViewSet(ModelViewSet):
    queryset = Categoria.objects.all()
    serializer_class = CategoriaSerializer


class EditoraViewSet(ModelViewSet):
    queryset = Editora.objects.all()
    serializer_class = EditoraSerializer
```

**`urls.py`**

```python
...
from core.views import CategoriaViewSet, EditoraViewSet
...
router.register(r"categorias", CategoriaViewSet)
router.register(r"editoras", EditoraViewSet)
...
```

**Teste da API da Editora**

-   Teste todas as operações da `Editora`.
-   Verifique se é possível incluir novas editoras sem incluir todos os campos.
-   Tente utilizar o PUT e o PATCH sem informar todos os campos.
-   Tente remover uma editora com livros associados a ela.

**Criação da API para Autor e Livro**

-   Repita os passos para a criação da API para `Autor` e `Livro`.
-   Teste o funcionamento.
-   Observe que no Livro, aparecem apenas os campos `id` da categoria e da editora.

**Apresentação das informações de categoria e editora no livro**

Uma forma de mostrar essas informações é essa, em `serializers.py`:

```python
class LivroSerializer(ModelSerializer):
    class Meta:
        model = Livro
        fields = "__all__"
        depth = 1
```

Teste e você verá que isso resolve a listagem (GET), mas gera problema no criação e alteração (POST, PUT e PATCH).

Para resolver isso, podemos criar dois (ou mais) serializadores, como no exemplo:

```python
class LivroSerializer(ModelSerializer):
    class Meta:
        model = Livro
        fields = "__all__"


class LivroDetailSerializer(ModelSerializer):
    class Meta:
        model = Livro
        fields = "__all__"
        depth = 1
```

Na viewset, escolhemos o serializador conforme a operação:

```python
class LivroViewSet(ModelViewSet):
    queryset = Livro.objects.all()

    def get_serializer_class(self):
        if self.action in ["list", "retrieve"]:
            return LivroDetailSerializer
        return LivroSerializer
```

# 9. Aplicação frontend Vuejs e Django CORS Headers

**Executando uma aplicação _frontend_ de exemplo**

Clone o repositório https://github.com/marrcandre/livraria-vue-3 e execute os seguintes comandos:

```shell
npm install
npm run dev
```

Se tudo correu bem, execute a aplicação:

http://localhost:3000

Se os dados não aparecerem, entre na opção **Inspecionar** do seu navegador (`Control`+`Shift`+I ou **botão direto - Inspecionar**.)

Na opção `Console`, verifique se aparece um erro de **CORS**. Se isso ocorrer, siga o tutorial a seguir.;

**Inclusão do Django CORS headers no projeto**

Adicionar o Django CORS headers permite que seu projeto seja acessado de outros domínios. Isso é necessário, por exemplo, para acessar a API através de uma aplicação de _frontend_ feita em _vuejs_.

-   Instale o pacote `django-cors-headers`:

```shell
pdm add django-cors-headers
```

-   Adicione o pacote `corsheaders` em `INSTALLED_APPS` em `settings.py`:

```python
INSTALLED_APPS = [
    ...,
    "corsheaders",
    "rest_framework",
    "core",
    ...,
]
```

Não esqueça da vírgula no final de cada linha e procure manter nessa mesma ordem.

-   Adicione o Middleware `corsheaders.middleware.CorsMiddleware` em `MIDDLEWARE` em `settings.py`:

```python
MIDDLEWARE = [
    ...,
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.common.CommonMiddleware",
    ...,
]
```

**IMPORTANTE**: a ordem aqui precisa ser essa.

Por fim, adicione a seguinte linha ao final do arquivo `settings.py`:

```python
CORS_ALLOW_ALL_ORIGINS = True
```

Feito isso, reinicie o servidor e tudo deve funcionar.

# 10. API REST do projeto Garagem

-   Volte ao projeto `Garagem`
-   Crie as classes, baseadas no arquivo `models.py` abaixo.
-   Depois, crie a API REST com o Django Rest Framework para todas as entidades.
-   Não esqueça de adicionar o DRF ao seu projeto.
-   Depois, teste tudo!

```python
class Categoria(models.Model):
    descricao = models.CharField(max_length=50)

    def __str__(self):
        return self.descricao


class Marca(models.Model):
    nome = models.CharField(max_length=50)

    def __str__(self):
        return self.nome


class Carro(models.Model):
    modelo = models.CharField(max_length=50)
    marca = models.ForeignKey(Marca, on_delete=models.PROTECT, related_name="carros")
    categoria = models.ForeignKey(
        Categoria, on_delete=models.PROTECT, related_name="carros"
    )
    ano = models.IntegerField(null=True, blank=True)
    cor = models.CharField(max_length=50, null=True, blank=True)
    preco = models.FloatField(null=True, blank=True)

    def __str__(self):
        return f"{self.marca} {self.modelo} {self.cor} ({self.ano})"
```

# 11. Relacionamento n para n

**Model com ManyToManyField - Livros com vários autores**

Um livro pode ter vários autores, por isso criaremos agora um relacionamento n para n entre `Livro` e `Autor`. Para isso utilizaremos um campo do tipo `ManyToManyField`.

-   Inclua o campo `autores` no modelo `Livro`:

```python
...
autores = models.ManyToManyField(Autor, related_name="livros")
...
```

-   Crie as migrações:

```shell
python manage.py makemigrations
```

-   Execute as migrações:

```shell
python manage.py migrate
```

Feito isso, observe no banco de dados que esse campo não foi criado na tabela de livros. Ao invés disso, uma **tabela associativa** foi criada, com o nome `core_livro_autores`, contendo os campos `livro_id` e `autor_id`. É assim que é feito um relacionamento n para n no Django.

**Tarefa**:

-   Entre no **Admin**;
-   Cadastre alguns autores;
-   Cadastre alguns livros com mais do que um autor.

# 12. Permissões de acesso

Vamos trabalhar agora os conceitos de segurança relacionados a **autenticação** (_login_) e **autorização** (_permissão_)). Utilizaremos aquilo que o Django
já oferece, em termos de usuários e grupos.

Uma estratégia muito utilizada para a definição de permissões de acesso é:

-   Criar **grupos** para perfis de usuários específicos
-   Definir as **permissões** que esse grupo de usuários terá
-   Criar um **usuário** para cada pessoa
-   **incluir** os usuários nos grupos, dando assim as permissões
-   No caso de mudanças nas permissões, elas são sempre feitas nos **grupos**, refletindo nos usuários
-   Se um usuário possui mais do que um perfil de permissões, ele deve ser incluído em **vários** grupos
-   Quando um usuário sai de um cargo ou deve perder seus privilégios, ele é **removido** do grupo específico

**Resumindo:** toda a estratégia de permissões parte da criação de grupos e inclusão ou remoção de usuários desses grupos.

Observe no **Admin**, para cada usuário em **Usuários (Users)**, as opções de **Permissões do usuário**.

**Criando grupos**

Vamos começar criando 2 grupos e dando a eles permissões distintas:

-   Crie um grupo chamado `compradores`, com as seguintes permissões:
    -   Visualizar: `autor`, `categoria` e `editora`.
    -   Adicionar, editar e visualizar: `livro`.
-   Crie um grupo chamado `administradores`, com as seguintes as permissões:
    -   Adicionar, editar, visualizar e remover: `autor`, `categoria`, `editora` e `livro`.

**Criando usuários e adicionando aos grupos**

-   Crie um usuário `admin1` e o inclua no grupo `administradores`.
-   Crie um usuário `comprador1` e o inclua no grupo `compradores`.

# 13. Usando as permissões do DRF

**Autenticação e permissão**

_A **autenticação** ou **identificação** por si só geralmente não é suficiente para obter acesso à informação ou código. Para isso, a entidade que solicita o acesso deve ter **autorização**._ [(Permissões no DRF)](https://www.django-rest-framework.org/api-guide/permissions/)

**Autenticação** significa que um usuário foi **identificado** em um sistema, portanto ele é **conhecido**. Isso se dá, normamente por um sistema de **_login_**.

**Permissão (autorização)** se dá por um esquema de **conceder privilégios**, seja a usuários ou grupos.

Por padrão, qualquer usuário, mesmo sem autenticação, tem acesso irrestrito e permissão de fazer qualquer coisa em uma aplicação.

As permissões podem ser definidas a nível de objeto (nas _views_ ou _viewsets_, por exemplo) ou de forma global, no arquivo `settings.py`.

**Exemplo de uso de permisssão na viewset**

Como ilustração, modifique o arquivo `views.py`, da seguinte forma.

-   Importe a seguinte função:

```python
from rest_framework.permissions import IsAuthenticated
```

-   Inclua também a seguinte linha na `CategoriaViewSet`:

```python
permission_classes = [IsAuthenticated]
```

Para testar:

-   Encerre a sessão do **Admin**
-   Tente acessar as **categorias** pelo DRF.
-   Você deve receber um erro.
-   Agora entre novamente pelo **Admin**.
-   Tente acessar as **categorias** pelo DRF.
-   Você deve conseguir.

**Exemplo de uso de permisssão no `settings.py`**

Outra forma de gerencimento de permissões é feita no arquivo `settings.py`. Para isso, utilizá-la, comente as últimas alterações feitas no arquivo `views.py`.

Uma forma de conseguir o mesmo resultado de forma padrão para todo o projeto, isto é, só permitir acesso a todos os _endpoints_ para usuários autenticados é configurar desse modo o arquivo `settings.py`:

```python
REST_FRAMEWORK = {
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.IsAuthenticated",
    ]
}
```

Inclua o código acima e teste novamente o acesso aos _endpoints_ do DRF (categorias, editoras, etc.) com e sem uma sessão autenticada.

**Permissões com o `DjangoModelPermissions`**

A forma que iremos adotar para o gerenciamento de permissões será com o uso do [DjangoModelPermissions](https://www.django-rest-framework.org/api-guide/permissions/#djangomodelpermissions).

Esta classe de permissão está ligada às permissões do modelo `django.contrib.auth` padrão do Django. Essa permissão deve ser aplicada apenas a visualizações que tenham uma propriedade `.queryset` ou método `get_queryset()` (exatamente o que temos).

A autorização só será concedida se o usuário estiver autenticado e tiver as permissões de modelo relevantes atribuídas, da seguinte forma:

-   As solicitações `POST` exigem que o usuário tenha a permissão de adição (`add`) no modelo.
-   As solicitações `PUT` e `PATCH` exigem que o usuário tenha a permissão de alteração (`change`) no modelo.
-   As solicitações `DELETE` exigem que o usuário tenha a permissão de exclusão (`remove`) no modelo.

Para isso, teremos que alterar a classe de autenticação:

```python
REST_FRAMEWORK = {
    ...
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.DjangoModelPermissions",
    ],
    ...
}
```

**Resumindo**, utilizaremos a estrutura de usuários, grupos e permissões que o próprio Django já nos fornece. Para isso, utilizaremos o `DjangoModelPermissions` para gerenciar as permissões.

Para utilizar essa estrutura de permissões corretamente, precisaremos de um sistema de autenticação (`login`) no nosso projeto, de forma a enviar essas informações via a `URL`. Utilizaremos o **SimpleJWT**.

# 14. Autenticação com o SimpleJWT

**Um resumo sobre autenticação e autorização**

Relembrando o que estudamos até aqui em termos de autenticação e autorização:

-   Como criar grupos e usuários e inserir os usuários nesses grupos
-   Como dar permissões nas models (via **Admin**) para visualização (`view`), adição (`add`), alteração (`change`) e exclusão (`remove`).
-   Como utilizar diversas formas de gerenciamento de permissões no Django, incluindo as permissões em cada `view` ou as permissões padrão no `settings.py`.
-   Como utilizar o `DjangoModelPermissions` para fazer uso do gerenciamento de permissões já incluído no **Django Admin**.

Agora, vamos utilizar o **SimpleJWT** para a autenticação no **Django REST Framework**.

**Resumindo**, utilizaremos o SimpleJWT para autenticação e a estrutura de permissões do Django para autorização.

**O SimpleJWT**

O [SimpleJWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/) é um plug-in de autenticação JSON Web Token para o Django REST Framework.

**Instalação**

-   Para instalar o SimpleJWT, execute o seguinte comando:

```shell
pdm add djangorestframework-simplejwt
```

**Configuração**

-   Adicione o `SimpleJWT` no arquivo `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "rest_framework_simplejwt",
    ...
]
```

-   Adicione o `SimpleJWT` no arquivo `urls.py`:

```python
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [
    ...
    path("token/", TokenObtainPairView.as_view(), name="token_obtain_pair"),
    path("token/refresh/", TokenRefreshView.as_view(), name="token_refresh"),
    ...
]
```

-   Adicione o `SimpleJWT` no arquivo `settings.py`:

```python
REST_FRAMEWORK = {
    ...
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),
    ...
}
```

Feitas essa aterações, coloque o servidor do Django novamente em execução.

Para testar se tudo deu certo, utilizaremos algum cliente HTTP, como **Postman**, **Insomnia**, **Thunder Client** ou **RapidAPI**.

# 15. Testando as permissões dos _endpoints_ usando um cliente HTTP

**Colocando as informações do token na requisição**

Feita a instalação e a configuração do SimpleJWT, podemos testar seu funcionamento. Para isso utilize um cliente HTTP.

**Dica:** se sua ferramenta permitir, crie várias requisições separadas para cada tipo de requisição, como autenticação, consulta, inclusão, etc.

-   Ao tentar acessar, por exemplo, o seguinte _endpoint_:

    http://localhost:8000/categorias/

-   Você deverá receber uma resposta parecida com essa:

```json
{
    "detail": "As credenciais de autenticação não foram fornecidas."
}
```

-   Para fazer a autenticação, precisamos enviar as informações de usuário e senha. Faremos isso enviando uma requisição do tipo `POST`, com as seguintes informações:

```json
{
    "username": "admin1",
    "password": "minhasenha1"
}
```

-   O endereço é o seguinte:

    http://localhost:8000/token/

**IMPORTANTE:** Não esqueça da barra (`/`) final no endereço e lembre-se que essa é uma requisição do tipo `POST`.

Você deve receber uma resposta semelhante a essa:

```json
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY2MTcyNDUxMCwiaWF0IjoxNjYxNjM4MTEwLCJqdGkiOiJiN2RhNWZkMjEwYTI0NjliOWE0MjgxZjQxZDcwNjZhMCIsInVzZXJfaWQiOjN9.lATd6io76oVa6nW5zuBEtsa8htvsL6wVhp-KzXMK-rk",
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjYxNjM4NDEwLCJpYXQiOjE2NjE2MzgxMTAsImp0aSI6ImRhYTBmNDcyZDI3YTQ5ZTM4M2I4ZjJhOTcwYjhlMWNmIiwidXNlcl9pZCI6M30.HY2j0L6eQBaPxAoHrPz_KFK_sWyb9lHmR7dQ1sOPTNY"
}
```

A cada chamada ao sistema, precisaremos enviar no cabeçalho da requisição um campo com o nome `Authorization` (autorização) com tipo `Bearer ` com essa chave que foi definida no campo `access`.

Para fazer isso, inclua em `Headers` um nova entrada, com se seguintes informações:

-   KEY (Header Name): `Authorization`
-   Value: `Bearer` + `valor da chave accesss`. (O valor desse token muda a cada nova autenticação.)
-   -   Por exemplo: `Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjYxNjM4NDEwLCJpYXQiOjE2NjE2MzgxMTAsImp0aSI6ImRhYTBmNDcyZDI3YTQ5ZTM4M2I4ZjJhOTcwYjhlMWNmIiwidXNlcl9pZCI6M30.HY2j0L6eQBaPxAoHrPz_KFK_sWyb9lHmR7dQ1sOPTNY`

Para testar, acesse com `GET` o seguinte endereço:

```
[GET] ​http://localhost:8000/categorias/
```

Você deverá conseguir visualizar todas as categorias cadastradas.

**_Token_ expirado**

```json
{
    "detail": "O token informado não é válido para qualquer tipo de token",
    "code": "token_not_valid",
    "messages": [
        {
            "token_class": "AccessToken",
            "token_type": "access",
            "message": "O token é inválido ou expirado"
        }
    ]
}
```

Recebemos essa mensagem quando o token expirou. Para isso, precisamos gerar um novo token.

**Testando com outro usuário**

Repita o processo de autenticação e consulta com o usuário `comprador1` que criamos anteriormente.

Resumindo, você vai precisar:

-   Criar uma requisição de autenticação, do tipo `POST`, para a URL `token`, enviando as informações de usuário e senha.
-   Copiar a chave do tipo `access` e colocá-la no cabeçalho `Authorization` da requisição do tipo `GET` que vocẽ fará.

**Tentando alterar uma informação**

```
[PUT] ​http://localhost:8000/categorias/10/
```

```json
{
    "descricao": "Cobol"
}
```

```json
{
    "detail": "Método \"PUT\" não é permitido."
}
```

Você não pode alterar uma informação com esse usuário. Para isso, você precisa de um usuário com permissão de escrita.

Com isso, fizemos um sistema básico de **autenticação** (_login_) e **autorização** (_permissões_) usando o próprio sistema já fornecido pelo Admin do Django.

# 16. Reestruturação em pastas de _models_, _views_ e _serializers_

Por padrão, as _models_, as _views_ e os _serializers_ são criados todos em um único arquivo, chamados respectivamente de `models.py`, `views.py` e `serializers.py`. Na medida em que o projeto vai crescendo e vão aumento o número de entidades, percebemos que é importante organizar essas entidades em arquivos separados. Obtemos com isso as seguintes vantagens:

-   Os arquivos ficam menores e mais fácil de encontrar o ponto correto de modificação.
-   Os conflitos no **GitHub** são evitados, pois normalmente as pessoas da equipe trabalham em entidades diferentes ao mesmo tempo.

Sendo assim, vamos fazer a separação dessas entidades em arquivos distintos, organizados dentro de uma pasta.

**IMPORTANTE:** essa mudança não afeta a forma de uso desses componentes, nem desempenho da aplicação e nem o banco de dados. É uma simples refatoração de código.

**Colocando os modelos em arquivos separados**

Siga os passos:

-   Crie uma pasta `models` dentro da pasta da aplicação (`livraria`):

```shell
mkdir core/models
```

-   Crie um arquivo `__init__.py` dentro da pasta `models` recém criada:

```shell
touch core/models/__init__.py
```

-   Crie um arquivo `autor.py` (será nossa primeira entidade) dentro da pasta `models`:

```shell
touch core/models/autor.py
```

-   Copie o conteúdo referente à entidade `Autor` do arquivo `models.py` para o arquivo `models/autor.py`.

```python
from django.db import models

class Autor(models.Model):
    nome = models.CharField(max_length=255)
    email = models.EmailField()

    def __str__(self):
        return self.nome

    class Meta:
        verbose_name_plural = "Autores"
```

-   Remova o conteúdo copiado no arquivo `models.py`. Não remova a linha do `import`, pois ela será utilizada por todas as entidades.
-   Inclua a importação da entidade `Autor` no arquivo `__init__.py`:

```python
from .autor import Autor
```

-   Repita os mesmos passos para as demais entidades (Categoria, Editora, Livro, etc.)
-   Observe que a entidade livro referencia as demais entidades, portanto elas precisam ser importadas em `livro.py`:

```python
from django.db import models

from core.models import Autor, Categoria, Editora


class Livro(models.Model):
...
```

-   Ao final desse processo o arquivo `model.py` deverá estar vazio e poderá ser removido. A aplicação deve continuar rodando perfeitamente.

**Separando _views_ e _serializers_ em arquivos**

Para separar as _views_ e os _serializers_ em arquivos, repita o mesmo processo feito para as _models_:

-   Crie a pasta correspondente (`views` e `serializers`).
-   Crie o arquivo `__init__.py` dentro de cada pasta.
-   Crie um arquivo para cada entidade dentro da pasta.
-   Copie o conteúdo do arquivo para o arquivo correspondente dentro da pasta.
-   Adicione a importação no arquivo `__init__.py`.
-   Remova o conteúdo do arquivo.

Ao final , você terá uma estrutura parecida com essa:

```
core
├── __init__.py
├── admin.py
├── apps.py
├── migrations
├── models
│   ├── __init__.py
│   ├── autor.py
│   ├── categoria.py
│   ├── editora.py
│   └── livro.py
├── serializers
│   ├── __init__.py
│   ├── autor.py
│   ├── categoria.py
│   ├── editora.py
│   └── livro.py
├── tests.py
└── views
    ├── __init__.py
    ├── autor.py
    ├── categoria.py
    ├── editora.py
    └── livro.py
```

A partir dessa organização, cada nova entidade criada terá seus arquivos correspondentes. Nada impede, no entanto, de agrupar entidades relacionadas em, um único conjunto de arquivos. Por exemplo, as entidades `Compra` e `ItensCompra` poderiam ficar em arquivos `compra.py`.

# 17. Adicionando campos ao usuário padrão do Django

Utilizaremos uma estratégia mais simples para a inclusão de campos ao usuário padrão do Django. Essa estratégia terá as seguintes características:

-   Substituiremos a classe `User` padrão do Django pela nossa própria classe `Usuario`.
-   Não removeremos os campos padrão do usuário.
-   Incluiremos os campos que precisamos no nosso usuário.
-   Teremos que remover o banco de dados e criar um novo, perdendo todos os dados.
-   Faremos a migração do banco de dados.
-   Modificaremos o Admin para que ele utilize a nossa classe `Usuario` e não a classe `User` padrão.

Vamos aos passos:

-   Crie um arquivo `usuario.py` dentro da pasta `models` da aplicação `livraria`.
-   Inclua o seguinte conteúdo:

```python
from django.db import models
from django.contrib.auth.models import AbstractUser


class Usuario(AbstractUser):
    cpf = models.CharField(max_length=11, unique=True)
    telefone = models.CharField(max_length=11, blank=True, null=True)
    data_nascimento = models.DateField(blank=True, null=True)
```

-   Adicione a importação no arquivo `__init__.py`:

```python
from .usuario import Usuario
```

-   Edite o arquivo `settings.py` e inclua a configuração abaixo:

```python
AUTH_USER_MODEL = "core.Usuario"
```

-   Remova o banco de dados e as migrações e crie novamente:

```shell
rm db.sqlite3
rm -rf core/migrations
python manage.py makemigrations core
python manage.py migrate
python manage.py createsuperuser
```

-   Edite o arquivo `admin.py` e inclua a configuração abaixo:

```python
...
from django.contrib.auth.admin import UserAdmin
from django.utils.translation import gettext_lazy as _
...

class UsuarioAdmin(UserAdmin):
    fieldsets = (
        (None, {"fields": ("username", "password")}),
        (_("Personal info"), {"fields": ("first_name", "last_name", "email", "cpf", "telefone", "data_nascimento")}),
        (
            _("Permissions"),
            {
                "fields": (
                    "is_active",
                    "is_staff",
                    "is_superuser",
                    "groups",
                    "user_permissions",
                ),
            },
        ),
        (_("Important dates"), {"fields": ("last_login", "date_joined")}),
    )

admin.site.register(Usuario, UsuarioAdmin)
```

-   Entre no Admin e crie um novo usuário. Observe que os campos `cpf`, `telefone` e `data_nascimento` foram incluídos.

# 18. Upload e associação de imagens

Vamos instalar uma aplicação para gerenciar o upload de imagens e sua associação ao nosso modelos.

**Configuração**

-   Baixe o arquivo compactado `uploader.zip`, que contém o código fonte da aplicação `uploader`, executando o seguinte comando no terminal:

```shell
wget https://github.com/marrcandre/django-drf-tutorial/raw/main/uploader.zip
```

-   Descompacte esse arquivo. Certifique-se de que ele esteja na pasta raiz do projeto:

```shell
unzip uploader.zip
```

<!-- - Remova a pasta `media` do arquivo `.gitignore`. -->

O projeto ficará com uma estrutura parecida com essa:

```
.
├── core
├── livraria
├── uploader
│   ├── models
│   │   ├── document.py
│   │   ├── image.py
│   │   └── __init__.py
│   ├── router.py
│   ├── serializers
│   │   ├── document.py
│   │   ├── image.py
│   │   └── __init__.py
├── static
└── utils
    └── files.py
```

-   Instalar os pacotes `python-magic` e `Pillow`:

```shell
pdm add python-magic Pillow
```

-   Adicione o pacote `uploader` na lista de `INSTALLED_APPS`, no `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "uploader",
    "core",
    ...
]
```

-   Ainda no `settings.py` faça as seguintes configurações:

```python
MEDIA_URL = "http://localhost:8000/media/"
MEDIA_ENDPOINT = "/media/"
MEDIA_ROOT = os.path.join(BASE_DIR, "media/")
FILE_UPLOAD_PERMISSIONS = 0o640
```

-   Inclua o seguinte conteúdo no arquivo `urls.py`:

```python
from django.conf import settings
from django.conf.urls.static import static
...
from uploader.router import router as uploader_router
...
path("api/media/", include(uploader_router.urls)),
...
urlpatterns += static(settings.MEDIA_ENDPOINT, document_root=settings.MEDIA_ROOT)
...
```

-   Faça a migração do banco de dados:

```shell
python manage.py makemigrations uploader
python manage.py migrate
```

**Uso em modelos**

-   Edite o arquivo `models/livro.py` da aplicação `livraria` e inclua o seguinte conteúdo:

```python
...
from uploader.models import Image


class Livro(models.Model):
...
    capa = models.ForeignKey(
        Image,
        related_name="+",
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        default=None,
    )
```

-   Faça novamente a migração do banco de dados:

```shell
python manage.py makemigrations core
python manage.py migrate
```

**Uso no serializer**

-   Edite o arquivo `serializers\livro.py` da aplicação `livraria` e inclua o seguinte conteúdo:

```python
...
from rest_framework.serializers import ModelSerializer, SlugRelatedField

from uploader.models import Image
from uploader.serializers import ImageSerializer
...
class LivroSerializer(ModelSerializer):
    capa_attachment_key = SlugRelatedField(
        source="capa",
        queryset=Image.objects.all(),
        slug_field="attachment_key",
        required=False,
        write_only=True,
    )
    capa = ImageSerializer(required=False, read_only=True)

...
class LivroDetailSerializer(ModelSerializer):
...
    capa = ImageSerializer(required=False)
```

**Teste de upload e associação com o livro**

-   Acesse a API de media:

    http://localhost:8000/api/media/images/

-   Faça o upload de uma imagem.
-   Observe que o campo `capa_attachment_key` foi preenchido com o valor `attachment_key` da imagem.
-   Guarde o valor do campo `capa_attachment_key`.
-   Crie um novo livro, preenchendo o campo `capa_attachment_key` com o valor guardado anteriormente.
-   Acesse o endpoint `http://localhost:8000/api/media/images/` e observe que a imagem foi associada ao livro.

# 19. Habilitando o Swagger e Redoc usando DRF Spectacular

Vamos instalar uma aplicação para gerar a documentação da API usando o Swagger e o Redoc.

**Instalação e Configuração**

-   Instale o pacote `drf-spectacular`:

```shell
pdm add drf-spectacular
```

-   Adicione o pacote `drf_spectacular` na lista de `INSTALLED_APPS`, no `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "drf_spectacular",
    ...
]
```

-   Registre o pacote no `settings.py`:

```python
REST_FRAMEWORK = {
    ...
    "DEFAULT_SCHEMA_CLASS": "drf_spectacular.openapi.AutoSchema",
}
```

-   Faça ainda algumas configurações no `settings.py`:

```python
SPECTACULAR_SETTINGS = {
    "TITLE": "Livraria API",
    "DESCRIPTION": "API para gerenciamento de livraria, incluindo endpoints e documentação.",
    "VERSION": "1.0.0",
}
```

-   Inclua o seguinte conteúdo no arquivo `urls.py`, **organizando-o adequadamente**:

```python
from drf_spectacular.views import (
    SpectacularAPIView,
    SpectacularRedocView,
    SpectacularSwaggerView,
)
...
urlpatterns = [
    ...
    # OpenAPI 3
    path("api/schema/", SpectacularAPIView.as_view(), name="schema"),
    path(
        "api/swagger/",
        SpectacularSwaggerView.as_view(url_name="schema"),
        name="swagger-ui",
    ),
    path(
        "api/redoc/",
        SpectacularRedocView.as_view(url_name="schema"),
        name="redoc",
    ),
]
```

**Teste**

-   Acesse o Swagger:

    http://localhost:8000/api/swagger/

**Alteração da URL da API**

-   Edite o arquivo `urls.py` altere a URL da API para `http://localhost:8000/api/`:

```python
urlpatterns = [
    ...
    path("api/", include(router.urls)),
    ...
]
```

# 21. Dump e Load de dados

Vamos aprender a fazer o _dump_ e _load_ de dados.

**Cópia de segurança dos dados**

-   Execute o comando `dumpdata`:

```shell
python manage.py dumpdata --indent 2 > livraria_bkp.json
```

-   Observe que o arquivo `livraria_bkp.json` foi criado:

```shell
code livraria_bkp.json
```

**Arquivo exemplo**

-   Baixe o arquivo `livraria.json`:

```shell
wget https://github.com/marrcandre/django-drf-tutorial/raw/main/livraria.json
```

**Carga dos dados**

-   Execute o comando `loaddata`:

```shell
python manage.py loaddata livraria.json
```

-   Observe que os dados foram carregados:

```shell
python manage.py shell
>>> from core.models import Livro
>>> Livro.objects.all()
```

Você também pode acessar o Django Admin ou o Swagger e verificar que os dados foram carregados.

# 22- Uso do Django Shell

O Django Shell é uma ferramenta para interagir com o banco de dados.

-   Acesse o shell:

```shell
python manage.py shell
```

-   Importe os modelos de `livraria.models`:

```python
>>> from core.models import Autor, Categoria, Editora, Livro
```

-   Crie um objeto:

```python
>>> categoria = Categoria.objects.create(descricao="Desenvolvimento Web")
```

-   Observe que o objeto foi criado:

```python
>>> categoria
<Categoria: Desenvolvimento Web>
```

-   Liste os objetos:

```python
>>> Categoria.objects.all()
<QuerySet [<Categoria: Desenvolvimento Web>]>
```

-   Obtenha o objeto:

```python
>>> categoria = Categoria.objects.get(descricao="Desenvolvimento Web")
```

-   Observe que o objeto foi obtido:

```python
>>> categoria
<Categoria: Desenvolvimento Web>
```

-   Atualize o objeto:

```python
>>> categoria.descricao = "Desenvolvimento Web com Django"
>>> categoria.save()
```

-   Observe que o objeto foi atualizado:

```python
>>> categoria
<Categoria: Desenvolvimento Web com Django>
```

-   Remova o objeto:

```python
>>> categoria.delete()
(1, {'core.Categoria': 1})
```

-   Observe que o objeto foi removido:

```python
>>> Categoria.objects.all()
<QuerySet []>
```

-   Acesso a todos os livros de um autor:

```python
Autor.objects.get(id=1).livros.all()
```

-   Acesso a todos os livros de uma categoria:

```python
Categoria.objects.get(id=1).livros.all()
```

-   Acesso a todos os livros de uma editora:

```python
Editora.objects.get(id=1).livros.all()
```

-   Encerre o shell:

```python
>>> exit()
```

# 23. Customização do Admin

O Admin é uma ferramenta para gerenciar os dados do banco de dados. Ele pode ser customizado para melhorar a experiência do usuário.

**Customização do Admin**

-   Edite o arquivo `livraria/admin.py`:

```python
...
@admin.register(Autor)
class AutorAdmin(admin.ModelAdmin):
    list_display = ('nome', 'email')
    search_fields = ('nome', 'email')
    list_filter = ('nome',)
    ordering = ('nome', 'email')

@admin.register(Categoria)
class CategoriaAdmin(admin.ModelAdmin):
    list_display = ('descricao',)
    search_fields = ('descricao',)
    list_filter = ('descricao',)
    ordering = ('descricao',)

@admin.register(Editora)
class EditoraAdmin(admin.ModelAdmin):
    list_display = ('nome',)
    search_fields = ('nome',)
    list_filter = ('nome',)
    ordering = ('nome',)

@admin.register(Livro)
class LivroAdmin(admin.ModelAdmin):
    list_display = ('titulo', 'editora', 'categoria')
    search_fields = ('titulo', 'editora__nome', 'categoria__descricao')
    list_filter = ('editora', 'categoria')
    ordering = ('titulo', 'editora', 'categoria')
    list_per_page = 25
```

-   Acesse o Admin:

    http://localhost:8000/admin/

# 24. Configurando variáveis de ambiente

É importante manter informações sensíveis, como chaves de API e senhas, longe de olhares indiscretos. A melhor maneira de fazer isso é não colocá-los no **GitHub**! Para isso, vamos usar o arquivo `.env` para armazenar essas informações.

-   Instale o pacote `django_environ`:

```shell
pdm add django-environ
```

-   Edite o arquivo `livraria/settings.py`:

```python
...
import environ
...
# Carrega as variáveis de ambiente do sistema operacional e as prepara para usá-las
env = environ.Env()
environ.Env.read_env((os.path.join(BASE_DIR, '.env')))

SECRET_KEY = env('SECRET_KEY')
DEBUG = env('DEBUG')
ALLOWED_HOSTS = env('ALLOWED_HOSTS').split(',')
DATABASES = {'default': env.db()}
```

IMPORTANTE: Após incluir essas variáveis, remova as outras referências a elas no arquivo `settings.py`.

-   Crie o arquivo `.env`:

```shell
touch .env
```

-   Edite o arquivo `.env`:

```python
SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
DATABASE_URL=sqlite:///db.sqlite3
```

**IMPORTANTE**:

-   Adicione o arquivo `.env` ao arquivo `.gitignore`.
-   Feito isso, esse arquivo não será mais versionado pelo Git.
-   Para ter um modelo de arquivo `.env`, crie um arquivo `.env.example` e adicione-o ao Git.

```shell
cp .env .env.example
```

# 25. Publicação no PythonAnywhere

O PythonAnywhere é um serviço de hospedagem de aplicações Python. Ele permite que você hospede seu projeto Django gratuitamente. Para isso, você precisa criar uma conta no PythonAnywhere e seguir os passos abaixo. Para publicar seu projeto no PythonAnywhere, você precisa ter uma conta no **GitHub**.

**Criação da conta no PythonAnywhere**

-   Crie uma conta no https://www.pythonanywhere.com/

**Criação do banco de dados no PythonAnywhere**

-   Crie o banco de dados em https://www.pythonanywhere.com/dashboard/, na opção `Databases`.
-   Anote as informações de conexão com o banco de dados:
    -   Host: `sua_conta.mysql.pythonanywhere-services.com`
    -   Database name: `seu_usuario_bd$seu_bd`
    -   Username: `seu_usuario_bd`
    -   Password: `sua_senha_bd`

**IMPORTANTE:**

-   Substitua `seu_usuario` pelo seu usuário do **GitHub**.
-   Substitua `seu_projeto` pelo nome do seu projeto no **GitHub**.
-   Substitua `sua_conta` pelo nome da sua conta no PythonAnywhere.
-   Substitua `seu_bd` pelo nome do seu banco de dados.
-   Substitua `seu_usuario_bd` pelo nome do seu usuário no banco de dados.
-   Substitua `sua_senha_bd` pela sua senha no banco de dados.

**Instalação do módulo `mysqlclient`**

-   Instale o pacote `libmysqlclient-dev`:

```shell
sudo apt install libmysqlclient-dev
```

O pacote `libmysqlclient-dev` é necessário para instalar o módulo `mysqlclient`.

-   Instale o módulo `mysqlclient`:

```shell
pdm add mysqlclient
```

O módulo `mysqlclient` é necessário para conectar o Django ao banco de dados MySQL.

**Configuração das variáveis de ambiente**

-   Crie um arquivo `.env` na pasta raiz (`/`) do seu usuario no PythonAnywhere. Você pode fazer isso pelo console ou pela interface web, na opção `Files`.

```python
SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
DEBUG=False
ALLOWED_HOSTS=sua_conta.pythonanywhere.com
DATABASE_URL=mysql://seu_usuario_bd:sua_senha_bd@sua_conta.mysql.pythonanywhere-services.com/seu_usuario_bd$seu_bd
```

-   Inclua o seguinte conteúdo no arquivo .virtualenvs/postactivate:

```shell
echo "Copiando o arquivo .env para a pasta do projeto..."
cp ~/.env ~/seu_usuario.pythonanywhere.com/
```

Esse comando copia o arquivo `.env` dentro da pasta do seu projeto no PythonAnywhere.

**Geração da SECRET_KEY**

-   Para gerar uma nova SECRET_KEY (chave secreta), a ser colocada no arquivo `.env`, execute o comando:

```shell
python -c "import secrets; print(secrets.token_urlsafe())"
```

-   Você também pode gerar uma nova chave secreta em https://djecrety.ir/
-   Para saber mais sobre a chave secreta, acesse a [documentação](https://docs.djangoproject.com/en/4.1/ref/settings/#secret-key) do Django.

IMPORTANTE:

-   Não esqueça de substituir a chave secreta pelo valor gerado.
-   Não esqueça de substituir os valores das variáveis de ambiente pelos seus valores.

**Criação da API Token**

-   Crie uma API Token em `Account` > `API Token` em https://www.pythonanywhere.com/dashboard/.

**Instalação do cliente do PythonAnywhere**

-   Acesse o console (terminal) do PythonAnywhere em https://www.pythonanywhere.com/consoles/

-   Instale o cliente do PythonAnywhere no console:

```shell
pip install pythonanywhere --user
```

**Criação do projeto no PythonAnywhere**

O script `pa_autoconfigure_django.py` autoconfigura o projeto Django no PythonAnywhere a partir de um repositório do **GitHub**:

-   Faz o clone do repositório do **GitHub**.
-   Cria um virtualenv.
-   Instala as dependências do projeto.
-   Cria uma webapp.
-   Cria o arquivo de configuração `wsgi.py`.
-   Adiciona os arquivos estáticos.

-   No console do PythonAnywhere, execute o comando abaixo, substituindo `https://github.com/seu_usuario/seu_projeto.git` pelo link do seu repositório no **GitHub** (aquele mesmo que você usou para clonar o projeto):

```shell
pa_autoconfigure_django.py --python=3.8 --nuke https://github.com/seu_usuario/seu_projeto.git
```

**Ativando o virtualenv (se necessário)**

-   Se necessário, no console, ative o `virtualenv`:

```shell
workon marcoandre.pythonanywhere.com
```

**Migrando o banco de dados**

-   No console, execute o comando abaixo para migrar o banco de dados:

```shell
python manage.py migrate
```

**Configuração do banco de dados no PythonAnywhere**

-   Carregue os dados iniciais:

```shell
python manage.py loaddata livraria.json
```

**Remoção do banco de dados local (se necessário)**

Para remover um banco de dados, acesse https://www.pythonanywhere.com/dashboard/, na opção `Databases` e digite:

```shell
drop database seu_usuario$seu_bd;
```

**IMPORTANTE:** Não esqueça de substituir `seu_usuario` e `seu_bd` pelos seus valores.

**Baixar novamente o projeto do **GitHub** (se necessário)**

-   Se você precisar atualizar o projeto do **GitHub**, sem precisar executar todo o processo novamente execute o comando:

```shell
git pull
```

-   Em caso de erro, execute o comando:

```shell
git checkout -- .
git clean -f -d
git pull
```

-   Se houverem alterações no arquivo `requirements.txt`, execute o comando:

```shell
pip install -r requirements.txt
```

-   Se houverem alterações nos modelos, faça a migração:

```shell
python manage.py migrate
```

# 26. Inclusão da foto de perfil no usuário

Vamos incluir a foto de perfil no usuário.

**Criação do campo de foto de perfil**

-   No arquivo `models\usuario.py`, inclua o campo `foto`:

```python
...
from uploader.models import Image
...
class Usuario(AbstractUser):
    foto = models.ForeignKey(
        Image,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        default=None,
    )
```

-   Faça as migrações:

```shell
python manage.py makemigrations core
python manage.py migrate
```

-   No arquivo `admin.py`, inclua o campo `foto`:

```python
...
class UsuarioAdmin(UserAdmin):
    ...
    "fields": ("first_name","last_name","foto",...),
    ...
```

-   Crie um serializador para o usuário:

```python
rom rest_framework.serializers import ModelSerializer, SlugRelatedField

from core.models import Usuario
from media.models import Image
from media.serializers import ImageSerializer


class UsuarioSerializer(ModelSerializer):
    foto_attachment_key = SlugRelatedField(
        source="foto",
        queryset=Image.objects.all(),
        slug_field="attachment_key",
        required=False,
        write_only=True,
    )
    foto = ImageSerializer(required=False, read_only=True)

    class Meta:
        model = Usuario
        fields = "__all__"
```

-   Inclua o novo serializador no arquivo
    `__init__.py` dos serializadores:

```python
from .usuario import UsuarioSerializer
```

-   Crie uma nova view para o usuário:

```python
from rest_framework.viewsets import ModelViewSet

from core.models import Usuario
from core.serializers import UsuarioSerializer


class UsuarioViewSet(ModelViewSet):
    queryset = Usuario.objects.all()
    serializer_class = UsuarioSerializer
```

-   Inclua a nova view no arquivo `__init__.py` das views:

```python
from .usuario import UsuarioViewSet
```

-   Inclua a nova view no arquivo `urls.py`:

```python
from core.views import UsuarioViewSet
...
router.register(r"usuarios", UsuarioViewSet)
```

**Testando**

-   Inclua uma foto de perfil em um usuário.

<!-- Aulas futuras -->

<!-- Incluir MEDIA_URL no tutorial de configuração do .env e de deploy-->

<!-- Testes -->
<!-- Pre commits -->
<!-- Django Filter -->
<!-- DRF para campos related_name -->
<!-- Vuejs com autenticação e autorização. -->
<!-- Populate script  -->
<!-- Model de compras integrando com Model User do Django  -->
<!-- Criar model StatusCompra -->
<!-- Criar model ItensCompra -->
<!-- Uso de TabularInline no Admin para Itens da Compra -->
<!-- Endpoint para listagem básica de Compras -->
<!-- Ajustes na visualização do status de compra e itens de compra -->
