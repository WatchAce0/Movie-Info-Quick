<script>
  import MovieSummary from './MovieSummary.svelte';
  import Footer from './Footer.svelte';
</script>

<div class="flex flex-col min-h-screen">
  <div class="flex-grow">
    <MovieSummary />

  </div>

  <Footer />
</div>


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

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>