<script>
  export let name;

  import { onMount } from "svelte";
  const API_KEY = "0425af7d9564474a95be3d6f3488ced8";
  const URL = `https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=${API_KEY}`;

  let articles = [];

  onMount(async function () {
    const response = await fetch(URL); //fetch data by using API
    const json = await response.json();
    articles = json["articles"];
  });
</script>

<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
  rel="stylesheet"
  integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
  crossorigin="anonymous"
/>
<main>
  <h1>The US daily news</h1>
  <div class="container">
    <div class="row">
      {#each articles as article}
        <div class="col-md-4">
          <div class="card">
            <img src={article.urlToImage} alt="" />
            <div class="card-body">
              <h3>
                <a href={article.url} target="_blank">{article.title}/a> </a>
              </h3>
              <p>{article.description}</p>
              <a href={article.url} target="_blank">Read more</a>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  img {
    height: 300px;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
