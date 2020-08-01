<script context="module">
  export async function preload({ params, query }) {
    const res = await this.fetch(
      `https://rickandmortyapi.com/api/character/${params.id}`
    );
    const data = await res.json();
    if (res.status === 200) {
      return { character: data };
    } else {
      this.error(res.status, data.message);
    }
  }
</script>

<script>
  export let character;

  console.log(character);
</script>

<style>
  .Character {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 2em;
    padding: 1em 2em;
    justify-items: center;
    width: 80%;
    margin: 0 auto;
    min-height: calc(100vh - 4.5em - 3.5em - 2em);
  }
  .Character > div {
    width: 100%;
  }
  .Character-preview {
    box-shadow: 0 0 0.3em 0 rgba(0, 0, 0, 0.3);
    border-radius: 0.3em;
    overflow: hidden;
  }
  .Character-preview img {
    width: 100%;
    height: 80%;
    object-fit: cover;
    display: block;
  }
  .Character-preview h1 {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-weight: bold;
    font-size: 1em;
    height: 20%;
  }
  .Character-preview,
  .Character-information {
    height: 50%;
  }
  .Character-information {
    box-shadow: 0 0 0.3em 0 rgba(0, 0, 0, 0.3);
    border-radius: 0.3em;
    overflow: hidden;
    padding: 0 2em;
  }
  .Character-information div {
    margin-top: 1.5em;
  }
  .Character-information p {
    font-weight: bold;
    font-size: 1.5em;
    margin: 0.5em 0;
  }
  .Character-information span {
    font-weight: normal;
    font-size: 0.8em;
  }
</style>

<svelte:head>
  <title>{character.name} | Rick and Morty</title>
</svelte:head>

<div class="Character">
  <div>
    <div class="Character-preview">
      <img src={character.image} alt={character.name} />
      <h1>{character.name}</h1>
    </div>
  </div>
  <div>
    <div class="Character-information">
      <div>
        <p>
          Episodes:
          <span>{character.episode.length}</span>
        </p>
        <p>
          Status:
          <span>{character.status}</span>
        </p>
        <p>
          Species:
          <span>{character.species}</span>
        </p>
        <p>
          Gender:
          <span>{character.gender}</span>
        </p>
        <p>
          Origin:
          <span>{character.origin.name}</span>
        </p>
        <p>
          Last Location:
          <span>{character.location.name}</span>
        </p>
      </div>
    </div>
  </div>
</div>
