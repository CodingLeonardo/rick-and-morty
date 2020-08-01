<script>
  export let id;
  export let image;
  export let name;
  export let status;
  export let species;

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
  .Character {
    box-shadow: 0 0 0.3em 0 rgba(0, 0, 0, 0.3);
    border-radius: 0.3em;
    overflow: hidden;
    text-decoration: none;
    background: white;
    transition: 0.49s ease;
  }
  .Character:hover {
    transform: scale(1.15);
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

<a href={`./character/${id}`} class="Character">
  <img src={image} alt={name} />
  <div class="Character-info">
    <h1>{name}</h1>
    <p>
      <span
        class="Character-icon"
        style={`background: ${getStatusColor(status)}`} />
      {status} - {species}
    </p>
  </div>
</a>
