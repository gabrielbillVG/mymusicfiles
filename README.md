<h1> 🎵 My Music 2022 </h1>

![MyMusic](https://github.com/gabrielbillVG/mymusicfiles/blob/main/ezgif.com-gif-maker%20(1)%20(5).gif)

<h2>Indice</h2>
<a href="#sobre"> Sobre o My Music </a>
<br>
<a href="#tecnologias"> Tecnologias Utilizadas no projeto </a>
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
<a href="#bancodedados"> Banco de Dados </a>
<br>
<a href="#testes"> Testes </a>
<br>
<br>
<p id="sobre"> O Projeto My Music 2022 é um sistema gerenciador de músicas utilizado para o Bootcamp de desenvolvedores Jr. da CI&T.
O objetivo do projeto é desenvolver uma api que gerencie as musicas favoritas do usuário por meio de uma playlist individual personalizável.</p>
<p> Possui como principais funcionalidades:</p>

<br>
<h3 id="tecnologias"> Tecnologias Utilizadas no Projeto My Music </h3>
<p> Optamos pela metodologia Clean Architecture como padrão de organização do código. Por default, o projeto utiliza Java 11, Spring Boot e Maven. Escolhemos utilizar a biblioteca Lombok para simplificar e deixar o código mais limpo. Para documentação, escolhemos o Swagger por sua praticidade e vasta documentação.</p>
<p> Para os testes, JUnity 5(default do projeto), Mockito e Jacoco </p>
<br>

<h3 id="buscamusica">Permitir o usuário a buscar novas músicas:</h3>
<br>

```
ENDPOINT: /api/v1/music?filtro={musica}
METODO: GET
PARAMS: 
KEY = filtro
Value = {musica}
```
Retorno:
<br>STATUS: 200 OK

```{
    "data": {
        "content": [
            {
                "id": "{musicaId}",
                "nome": "{musicName}",
                "artista": {
                    "id": "{artistId}",
                    "name": "{artistName}"
                }
            }...
```


1. O serviço valida se o usuário informou ao menos 2 caracteres, retornando um HTTP 400
   caso a consulta tenha menos de 2 caracteres.

2. A busca é realizada através do nome de artista e nome da música.

3. A busca por música não é case sensitive.

4. A busca retorna valores contendo o filtro, não necessitando de ser informado o nome
   completo de música ou artista.

5. O retorno é ordenado pelo nome do artista e depois pelo nome da música.

<br>

<h3 id="addplaylist"> Permitir adicionar as músicas favoritas do usuário na playlist </h3>
Utilizar o endpoint a seguir:

```
ENDPOINT: /api/playlists/{Playlistid}}/musics
METODO: POST
BODY: 
{
  "data": [
  {
     "id": "fc615aa1-8f3a-499b-a422-9655d4a29006",
     "name": "Ani Na'amin",
     "artist": {
       "id": "2154a968-f48c-4890-a70f-a2c552c84b71",
       "name": "ABBA" 
      } 
  }
]}
```
Retorno:
<br>STATUS: 200 OK
```
{
        "data": [
            {
                "id": "fc615aa1-8f3a-499b-a422-9655d4a29006",
                "name": "Ani Na'amin",
                "artist": {
                    "id": "2154a968-f48c-4890-a70f-a2c552c84b71",
                    "name": "ABBA"
                }
            }
        ]
}
```


1. Recebe um request contendo o identificador da música e o identificador da playlist.

2. Valida se o identificador da música e o identificador da playlist existem.
<br>

<h3 id="removermusica"> Permitir o usuário remover músicas de sua playlist:</h3>

Utilizar o endpoint a seguir:

```
ENDPOINT: /api/playlists/{playlistId}/musics/{musicId}
METODO: DELETE

```
Retorno:
<br>STATUS: 200 OK
```

{
    "playlistId": "{playlistId}",
    "musicId": "{musicId}",
    "message": "Successful deletion"
}
```

1. Deve receber um request contendo o identificador da música e o identificador da playlist.


2. Deve validar se o identificador da música e o identificador da playlist existem.

<br>

<h1 id="endpoints"> Endpoints </h1>
Todos os endpoints devem possuir uma camada de segurança para proteger o dominio de dados. Para implementar
essa segurança os endpoints criados devem exigir que as requisições recebidas possuam o header "authorization",
contendo um token válido para responder a requisição. Para realizar a criação e geração do token, utilizar o serviço
disponbilizado junto com estrutura do projeto: token-provider-0.0.1-SNAPSHOT.jar.

<h1 id="token"> 🔒 Token-Provider</h1>

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

<br>

<h1 id="bancodedados"> Banco de Dados </h1>

Para auxiliar o desenvolvimento do API, a estrutura inicial conta com uma base de dados pré-definida e populada

Modelagem:
<div align="center"><img src="https://i.imgur.com/yfMGrur.png" title="source:modelagem imgur" /></div>

Atenção:
Os campos Id que utilizam GUID mapear como string devido à complexidade na compatibilidade com o UUID nativo do Java.

Dica:
Não é necessário, porém é possível utilizar uma ferramenta para abrir e visualizar o arquivo MyMusic.db de maneira mais
fácil, como:

https://sqlitestudio.pl/index.rvt

<br>

<h1 id="testes"> Testes </h3>
