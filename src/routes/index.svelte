<script>
  import { onMount } from "svelte";

  let characters;

  const fetchCharacters = async () => {
    const response = await fetch("https://rickandmortyapi.com/api/character/");
    const data = await response.json();
    characters = data.results;
    console.log(characters);
  };

  onMount(async () => {
    fetchCharacters();
  });

  const getStatusColor = status => {
    if (status === "Alive") {
      return "rgb(85, 204, 68)";
    }
    if (status === "Dead") {
      return "rgb(214, 61, 46)";
    }
    if (status === "unknown") {
      return "rgb(158, 158, 158)";
    }
  };
</script>

<style>
  .Home-hero {
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: url("./images/hero.png");
    background-size: 100%;
    background-position: center;
    background-repeat: no-repeat;
    height: calc(60vh - 4.5em);
  }
  .Home-hero h1 {
    color: white;
    font-size: 5em;
    font-weight: bold;
    text-shadow: 0 0.1em 0 rgba(0, 0, 0, 0.8);
  }
  .Home-characters {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(14em, 1fr));
    gap: 1em;
    margin: 0 auto;
    width: 80%;
    padding: 3em 0;
  }
  .Character {
    box-shadow: 0 0 0.3em 0 rgba(0, 0, 0, 0.3);
    border-radius: 0.3em;
    overflow: hidden;
    text-decoration: none;
    background: white;
    transition: 0.49s;
  }
  .Character:hover {
    transform: scale(1.2);
  }
  .Character img {
    width: 100%;
    height: 12em;
    object-fit: cover;
  }
  .Character-info {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    text-align: center;
  }
  .Character-info h1 {
    font-size: 1.2em;
    font-weight: bold;
    margin-top: 0.5em;
  }
  .Character-info p {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .Character-icon {
    display: block;
    width: 0.4em;
    height: 0.4em;
    border-radius: 50%;
    background: rgb(158, 158, 158);
    margin: 0;
    margin-right: 0.3em;
  }
</style>

<svelte:head>
  <title>Home | Rick and Morty</title>
</svelte:head>

<div class="Home">
  <div class="Home-hero">
    <h1>Characters</h1>
  </div>
  <div class="Home-characters">
    {#if characters}
      {#each characters as character}
        <a href={`./character/${character.id}`} class="Character">
          <img src={character.image} alt={character.name} />
          <div class="Character-info">
            <h1>{character.name}</h1>
            <p>
              <span
                class="Character-icon"
                style={`background: ${getStatusColor(character.status)}`} />
              {character.status} - {character.species}
            </p>
          </div>
        </a>
      {:else}
        <h1>Loading...</h1>
      {/each}
    {/if}
  </div>
</div>
