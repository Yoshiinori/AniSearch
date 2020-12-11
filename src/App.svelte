<script>
	let title;
	let details;
	let list = [];
	const getAnime = () => {
		fetch(`https://api.jikan.moe/v3/search/anime?q=${title}`)
		.then(res => res.json())
		.then(data => {
			console.log(data.results)
			list = data.results
		})
	};

	const submit = key => {
		if (key.charCode === 13) getAnime();
	};
</script>

<style>
	:global(body) {
		background-color: rgb(248, 204, 6);
	}

	.size {
		width: 25%;
	}

	.img-fluid {
		max-width: 75%;
	}
	
	@media (max-width: 768px) {
		.size {
			width: 100%;
		}
		.img-fluid {
			max-width: 100%;
		}
	 }

</style>

<div class="d-flex justify-content-center text-center container-fluid">
	<div>
		<img class="img-fluid" src="images/banner.png" alt="banner">
		<div class="mt-4 mb-4">
			<input on:keypress={submit} class="form-control col-lg-10 col-md-8 col-sm-6" type="text" name="title" bind:value={title} placeholder=
			"Anime Name" aria-label="Search!" aria-describedby="searchButton">
			<button class="btn btn-dark col-lg-2 col-md-4 col-sm-6" id="searchButton" on:click={getAnime}>
				Search!
			</button>
  	</div>
		<h3>Search for: {title}</h3>
	</div>
</div>

<div class="d-flex flex-wrap justify-content-center container-fluid">
{#each list as anime}
	<div class="card text-white rounded shadow-lg bg-dark size m-3">
	<img src={anime.image_url} class="card-img-top" alt="...">
	<div class="card-body">
		<h5 class="card-title">{anime.title}</h5>
		<p class="card-text">{anime.synopsis}</p>
	</div>
	</div>
{:else}
	<h1>Not Found</h1>
{/each}
</div>
