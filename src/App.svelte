<script>
	export let name;
	import { onMount } from 'svelte';

	const API_KEY = '<API KEY>';
	const URL = `https://newsapi.org/v2/everything?q=comics&sortBy=publishedAt&apiKey=${API_KEY}`;

	let articles = [];

	onMount(async function() {
        const response = await fetch(URL);
        const json = await response.json();
        articles = json["articles"];
    });
</script>

<style>
	h1 {
    color: purple;
    font-family: 'kalam';
}

.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(305px, 1fr));
    grid-gap: 15px;
}

.container > .card img {
    max-width: 100%;
}
</style>

<h1>
    <img src="https://dailyplanetdc.files.wordpress.com/2018/12/cropped-daily-planet-logo.jpg?w=656&h=146" alt='logo' />
    <p class="about">
            The Daily Planet is where heroes are born and the story continues. We are proud to report on the planet, daily.
    </p>
</h1>

<div class="container">

        {#each articles as article}
            <div class="card">
                <img src="{article.urlToImage}" alt='image'/>
                <div class="card-body">
                    <h3>{article.title}</h3>
                    <p> {article.description} </p>
                    <a href="{article.url}">Read story</a>
                </div>
            </div>
        {/each}

</div>
