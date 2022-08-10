# My Music 2022

![MyMusic] (https://github.com/gabrielbillVG/mymusicfiles/blob/main/ezgif-5-34f5820e19.gif)

<h2>Indice</h2>
<a href="#sobre"> Sobre </a>
<br>
<a href="#buscamusica"> Permitir o usuário a buscar novas músicas </a>
<br>
<a href="#addplaylist"> Permitir adicionar as músicas favoritas do usuário na playlist </a>
<br>
<a href="#removermusica"> Permitir o usuário remover músicas de sua playlist </a>
<br>
<a href="#endpoints"> Endpoints </a>
<br>
<a href="#token"> Token Provider </a>
<br>
<br>
<p id="sobre"> O Projeto My Music 2022 é um sistema gerenciador de músicas utilizado para o Bootccamp de desenvolvedores Jr. da CI&T.
O objetivo do projeto é desenvolver uma api que gerencie as musicas favoritas do usuário por meio de uma playlist individual personalizável.</p>
<p> Possui como principais funcionalidades:</p>

<h1 id="buscamusica">Permitir o usuário a buscar novas músicas:</h1>

1. O serviço deve validar se o usuário informou ao menos 3 caracteres, retornando um HTTP 400
   caso a consulta tenha menos de 3 caracteres.
2. A busca deve ser realizada através do nome de artista e nome da música.
3. A busca por música não deve ser case sensitive.
4. A busca deve retornar valores contendo o filtro, não necessitando de ser informado o nome
   completo de música ou artista.
5. O retorno deve estar ordenado pelo nome do artista e depois pelo nome da música.

<h1 id="addplaylist"> Permitir adicionar as músicas favoritas do usuário na playlist:</h1>

1. Deve receber um request contendo o identificador da música e o identificador da playlist.
2. Deve validar se o identificador da música e o identificador da playlist existem.

<h1 id="removermusica"> Permitir o usuário remover músicas de sua playlist:</h1>

3. Deve receber um request contendo o identificador da música e o identificador da playlist.
4. Deve validar se o identificador da música e o identificador da playlist existem.


<h1 id="endpoints"> Endpoints </h1>
Todos os endpoints devem possuir uma camada de segurança para proteger o dominio de dados. Para implementar
essa segurança os endpoints criados devem exigir que as requisições recebidas possuam o header "authorization",
contendo um token válido para responder a requisição. Para realizar a criação e geração do token, utilizar o serviço
disponbilizado junto com estrutura do projeto: token-provider-0.0.1-SNAPSHOT.jar.

<h3 id="token"> Token-Provider</h3>

Para criação de token válidos utilizar o endpoint a seguir:

```
ENDPOINT: /api/v1/token
METODO: POST
BODY: 
{ 
    "data": {
        "name": "fulano"
    }
}
RETORNO: 201 Created
{
    "12321312321312"
}
```

Para validação de token utilizar o endpoint a seguir:

```
ENDPOINT: /api/v1/token/authorizer
METODO: POST
BODY: 
{ 
    "data": {
        "name": "fulano",
        "token": "12321312321312"
    }
}
RETORNO: 201 Created
{
    "ok"
}
```

# Banco de dados

Para auxiliar o desenvolvimento do API, a estrutura inicial conta com uma base de dados pré-definida e populada

Modelagem:
<div align="center"><img src="https://i.imgur.com/yfMGrur.png" title="source:modelagem imgur" /></div>

Atenção:
Os campos Id que utilizam GUID mapear como string devido à complexidade na compatibilidade com o UUID nativo do Java.

Dica:
Não é necessário, porém é possível utilizar uma ferramenta para abrir e visualizar o arquivo MyMusic.db de maneira mais
fácil, como:

https://sqlitestudio.pl/index.rvt

