# PZM-teste-Pokemon
Uma mini aplicação que gera pokémons da primeira geração aleatoriamente, permitindo visualizar os últimos pokémons que foram gerados e opcionalmente renomea-los.
Linguaguens utilizadas foram HTML,CSS e Java Script.

HTML:
<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Busca Pokemon</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h1>Trabalhando com <strong>HTML</strong>, <strong>CSS</strong> e usando o <strong>JavaScript</strong> para
            fazer consultas online.</h1>
        <hr>
        <div class="imagem">
            <img src="img/pokemon-logo.png">
        </div>
        <form>
            <div class="group-form">
                <label>Nome ou Número do Pokémon:</label>
                <input type="text" id="name" placeholder="Exemplo: Pikachu ou 25" required>
            </div>
            <div class="group-form">
                <input type="submit" value="Pesquisar">
            </div>
        </form>
        <div id="imgPokemon">
        </div>
        <div id="content">...</div>
    </div>
    <script src="script.js"></script>
</body>

</html>


Java Script:
var formulario = document.querySelector('form')

formulario.addEventListener('submit', function (e) {

    // Bloqueia o refresh da página
    e.preventDefault()

    // Url da pesquisa
    let urlForm = "https://pokeapi.co/api/v2/pokemon/";

    // Valor do inpt Name
    let nome = document.getElementById("name")

    // Concatena a url com o inputname
    urlForm = urlForm + this.name.value

    // Transforma os valores em minúsculas
    urlForm = urlForm.toLocaleLowerCase()

    // ID Content
    let resposta = document.getElementById('content')

    // Id ImgPokemon
    let imagem = document.getElementById('imgPokemon')

    // Resposta em HTML
    let html = ''

    fetch(urlForm)
        .then(resposta => resposta.json())
        .then(function (data) {

            html = 'Nome: ' + maiuscula(data.name) + '<br>'
            html = html + 'Type: ' + maiuscula(data.types[0].type.name)
            resposta.innerHTML = html

            imagem.innerHTML = "<img src='" + data.sprites.front_default + "'><img src='" + data.sprites.back_default + "'>"
        })
        .catch(function (err) {
            if(err == 'SyntaxError: Unexpected token N in JSON at position 0'){
                html = 'Pokémon não encontrado! 😒'
            } else {
                html = err
            }
            resposta.innerHTML = html
        })
});

function maiuscula(val){
    return val[0].toUpperCase() + val.substr(1)
}


CSS:
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;900&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html,
body {
    width: 100%;
    height: 100%;
}

body {
    font-family: Poppins;
    background: #F5F5F5;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}

h1 {
    font-size: 20px;
    text-align: center;
}

strong {
    color: #2F67B2;
}

hr {
    margin: 10px 0;
    border-top: 3px solid #CCC;
    border-radius: 5px;
}

.container {
    border: 1px solid #CCC;
    border-radius: 10px;
    padding: 20px;
    background: #FFF;
    max-width: 450px;
    min-height: 300px;
}

.imagem,
#imgPokemon {
    text-align: center;
    min-height: 50%;
}

.imagem img {
    width: 90%;
}

.group-form {
    padding: 5px 0;
}

.group-form label {
    font-weight: 900;
    color: #1b356e;
}

.group-form input {
    width: 100%;
    padding: 10px;
    border: 1px solid #CCC;
    border-radius: 5px;
    font-family: Poppins;
    text-transform: uppercase;
}

.group-form input[type=submit] {
    background-color: #1B356E;
    font-weight: 600;
    color: #FFF;
    font-size: 1rem;
    letter-spacing: 1px;
    cursor: pointer;
}

#imgPokemon img {
    width: 90px;
    border-radius: 50%;
    border: 1px solid #333;
    margin: 10px;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, .3);
}

#content {
    font-family: monospace;
    padding: 10px;
    background-color: #FFCC01;
    border: 1px solid #c8a102;
    border-radius: 5px;
    font-weight: 900;
    font-size: 1rem;
    text-align: center;
    color: #333;
}
