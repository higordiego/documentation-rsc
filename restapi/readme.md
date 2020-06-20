# Contratos de Chamadas de API


# Métodos HTTP
Utilizaremos os seguintes [metodos HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods):
* - [x] **OPTIONS** - ```O método OPTIONS é usado para descrever as opções de comunicação com o recurso de destino.```
* - [x] **POST** - ```O método POST é utilizado para submeter uma entidade a um recurso específico, frequentemente causando uma mudança no estado do recurso ou efeitos colaterais no servidor.```
* - [x] **PUT** - ```O método PUT substitui todas as atuais representações do recurso de destino pela carga de dados da requisição.```
* - [x] **GET** - ```O método GET solicita a representação de um recurso específico. Requisições utilizando o método GET devem retornar apenas dados.```
* - [x] **DELETE** - ```O método DELETE remove um recurso específico.```


# Formato de comunicação de dados.

Para envio de dados vamos utilizar o formato [JSON](https://www.devmedia.com.br/o-que-e-json/23166).

```JSON é basicamente um formato leve de troca de informações/dados entre sistemas. Mas JSON significa JavaScript Object Notation.```

# Assinaturas de envio.

Esses são os tipos de envios que será abordado na comunicação de Front-end com Back-end.

## Método POST
No método [POST](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/POST) iremos utilizar o seguinte formato:

URL de envio:
```fetch
http://host/criar
```

Envio dos dados
```json
{
 "name_example": "example",
 "idade": "19"
}
```

Utilizaremos POST quando o contrato tenha o intuito de:
* [x] Criação
* [x] Autenticação
* [x] Envio de dados sensíveis

## Método GET
No método [GET](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/GET) iremos utilizar o seguinte formato:

URL de envio
```fetch
http://host/consultar?nome=teste
```

Utilizaremos GET quando o contrato tenha o intuito de:
* [x] Consulta

## Método PUT
No método [PUT](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/PUT) iremos utilizar o seguinte formato:

URL de envio:
```fetch
http://host/alterar/10
```

Envio dos dados
```json
{
 "name_example": "example",
 "idade": "19"
}
```

Utilizaremos PUT quando o contrato tenha o intuito de:
* [x] Alteração dos dados


## Método DELETE
No método [DELETE](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/DELETE) iremos utilizar o seguinte formato:

URL de envio:
```fetch
http://host/alterar/10
```

Utilizaremos DELETE quando o contrato tenha o intuito de:
* [x] Para deletar os dados

# Verbos HTTP
```O protocolo HTTP define métodos (às vezes referidos como verbos) para indicar a ação desejada a ser realizada no recurso identificado. O que este recurso representa, se são dados pré-existentes ou dados gerados dinamicamente, depende da implementação do servidor. Muitas vezes, o recurso corresponde a um arquivo ou a saída de um executável residente no servidor. (fonte Wikipedia)```

Utilizaremos os seguintes [verbos HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status):

* - [x] **201** - ```A requisição foi bem sucedida e um novo recurso foi criado como resultado. Esta é uma tipica resposta enviada após uma requisição POST.```
* - [x] **200** - ```Estas requisição foi bem sucedida. O significado do sucesso varia de acordo com o método HTTP```
* - [x] **400** - ```Essa resposta significa que o servidor não entendeu a requisição pois está com uma sintaxe inválida.```
* - [x] **401** - ```Embora o padrão HTTP especifique "unauthorized", semanticamente, essa resposta significa "unauthenticated". Ou seja, o cliente deve se autenticar para obter a resposta solicitada.```
* - [x] **404** - ```O servidor não pode encontrar o recurso solicitado. Este código de resposta talvez seja o mais famoso devido à frequência com que acontece na web.```
* - [x] **403** - ```O cliente não tem direitos de acesso ao conteúdo portanto o servidor está rejeitando dar a resposta. Diferente do código 401, aqui a identidade do cliente é conhecida.```
* - [x] **500** - ```O servidor encontrou uma situação com a qual não sabe lidar.```

Todos os responses da API terá que vim no status code do [headers](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers).


# Retorno Esperados
Retorno da API em caso de [Status Code](https://httpstatuses.com/) 200/201.

```json
{
    "data": {}
}
```

Retorno da API em caso de [Status Code](https://httpstatuses.com/) 400 com parâmetros inválidos ou nulos.

```json 
{
  "errors": [
          { 
            "message": "O campo '{parametro}' inválido.",
          }
    ]
}
```


Retorno da API em caso de [Status Code](https://httpstatuses.com/) 404 com erro.

```json
  {
    "errors":  [
      {
          "message": "Endpoint não encontrado.",
      }
    ]
  }
```

Retorno da API em caso de [Status Code](https://httpstatuses.com/) 401 com erro.

```json
{
  "errors": [
        {
            "message": "O login falhou. Verifique se os dados informados estão corretos.",
        }
    ]
}
```


Retorno da API em caso de [Status Code](https://httpstatuses.com/) 403 com erro.

```json
  {
    "errors": [
          {
              "message": "O usuário sem permissão para essa ação.",
          }
      ]
  }
```

Retorno da API em caso de [Status Code](https://httpstatuses.com/) 500 com erro.

```json
  {
    "errors": [
          {
              "message": "Estamos passando por instabildade, por favor tente novamente!",
          }
      ]
  }
```

# Tempo de requisição
As requisições feitas para API terá o [timeout](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status/408) de 3 segundos.


