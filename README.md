# Prova de Conceito: Fetch
Este projeto é uma aplicação web simples que exibe informações detalhadas sobre os 151 primeiros Pokémons, utilizando a PokeAPI. Ele renderiza o nome, imagem, número, altura, peso e tipos de cada Pokémon em um cartão estilizado
## Funcionalidades
- Exibir cartões com informações detalhadas sobre cada um dos primeiros 151 Pokémons.
- Redirecionar o usuário para a página index.html ao clicar em um botão "Voltar".
# Estrutura do Projeto
- index.html: Estrutura básica contendo o conteúdo da API
- api.js: Contém os dados com informações de 151 Pokémons
- api.css: Estilização da pagina que contém os dados da API
# Estrutura do Código 
### 1. Redicionamento com botão
   ``` js
   const botao = document.getElementById('voltar');
   botao.addEventListener('click', () => {
   window.location.href = 'index.html';
   });
   ``` 
Este trecho de código seleciona o botão com o id voltar e adiciona um evento click a ele. Quando o botão é clicado, o usuário é redirecionado para a página index.html.

### 2. Função de Requisição à PokeAPI
``` js
const fetchPokemon = async () => {
  const response = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=151`);
  const data = await response.json();
  
  const detalhePokemon = await Promise.all(data.results.map(async (pokemon) => { 
    const response = await fetch(pokemon.url);
    return await response.json(); 
  }));
  
  return detalhePokemon;
}
```
Esta função faz uma requisição à PokeAPI para buscar os primeiros 151 Pokémons e, para cada um, obtém mais detalhes, como imagem, altura, peso e tipos. Ela utiliza Promise.all para lidar com as múltiplas requisições.

### 3. Função para Exibir os Pokémons
``` js
const exibirPokemon = async () => {
  const pokemons = await fetchPokemon();

  pokemons.forEach(pokemon => {
    const pokemonDiv = document.createElement('div');
    pokemonDiv.classList.add('pokemon');

    const name = document.createElement('h1');
    name.textContent = pokemon.name;
    pokemonDiv.appendChild(name);

    const image = document.createElement('img');
    image.src = pokemon.sprites.front_default;
    pokemonDiv.appendChild(image);

    const id = document.createElement('p');
    id.textContent = `Nº: ${pokemon.id}`;
    pokemonDiv.appendChild(id);

    const height = document.createElement('p');
    height.textContent = `height: ${(pokemon.height / 10).toFixed(2)} m`;
    pokemonDiv.appendChild(height);

    const weight = document.createElement('p');
    weight.textContent = `weight: ${(pokemon.weight / 10).toFixed(2)} kg`;
    pokemonDiv.appendChild(weight);

    const types = document.createElement('p');
    types.textContent = `type: ${pokemon.types.map(typeInfo => typeInfo.type.name).join(', ')}`;
    pokemonDiv.appendChild(types);

    pokemonCard.appendChild(pokemonDiv);
  });
}
```
Esta função cria elementos HTML dinamicamente para exibir as informações de cada Pokémon na página. Ela utiliza o array de Pokémons retornado pela função fetchPokemon e cria uma estrutura HTML para exibir as informações.

### 4. Chamada inicial
``` js
exibirPokemon();
```
A função exibirPokemon() é chamada para iniciar o processo de carregamento e exibição dos Pokémons na página ao carregar o script.
## Observações
Este projeto utiliza a PokeAPI e, portanto, requer uma conexão com a internet para buscar as informações dos Pokémons.

### Imagens do Projeto 
## ![Pokemons](https://github.com/ArthurEdu05/POC4-fetch-TechMack/blob/main/Imagens%20da%20Api/apiPokemon.png)
## ![Async/Await](https://github.com/ArthurEdu05/POC4-fetch-TechMack/blob/main/Imagens%20da%20Api/api2.png)
## ![Exemplo de um Card](https://github.com/ArthurEdu05/POC4-fetch-TechMack/blob/main/Imagens%20da%20Api/api3.png)
 ![Lista Executada](https://github.com/ArthurEdu05/POC4-fetch-TechMack/blob/main/Imagens%20da%20Api/api4.png)

## Tecnologias Utilizadas 
- HTML5
- JavaScript (ES6+)
- PokeAPI para obter dados dos Pokémons
- CSS

## Autores
- Arthur Eduardo - 10437356
- Felipe Melantonio - 10443843
- Guilherme Sampaio Silva - 10443768
