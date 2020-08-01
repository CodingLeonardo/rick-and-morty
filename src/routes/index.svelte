<script>
  import { onMount } from "svelte";
  import Character from "../components/Character.svelte";

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
        <Character
          name={character.name}
          image={character.image}
          id={character.id}
          status={character.status}
          species={character.species} />
      {:else}
        <h1>Loading...</h1>
      {/each}
    {/if}
  </div>
</div>
