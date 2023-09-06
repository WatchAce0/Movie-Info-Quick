<script>
  let movieTitle = "";
  let movieData = null;
  let errorMessage = "";

  const API_KEY = "400774ef"; // Replace with your own OMDB API key

  async function searchMovie() {
    if (movieTitle.trim()) {
      try {
        const response = await fetch(
          `https://www.omdbapi.com/?t=${movieTitle}&apikey=${API_KEY}`
        );
        const data = await response.json();

        if (data.Response === "True") {
          movieData = data;
          errorMessage = "";
        } else {
          movieData = null;
          errorMessage = data.Error;
        }
      } catch (error) {
        console.error("Error fetching movie data:", error);
        errorMessage = "Unable to fetch movie data. Please try again later.";
      }
    } else {
      errorMessage = "Please enter a movie title.";
    }
  }
</script>
<div class="container max-w-md mx-auto p-4 bg-white shadow-lg rounded-lg mt-20">
  <h1 class="text-4xl font-bold mb-6 text-center">Movie Info Quick</h1>
   <h2 class="text-lg font-light mb-6 text-center"> Enter the title of the Movie you would like more information about and hit Search. </h2>
  <div class="flex items-center justify-center mb-4">
   <input
  bind:value={movieTitle}
  type="text"
  class="flex-grow border border-gray-300 p-3 rounded-l-lg focus:outline-none focus:ring focus:border-blue-300"
  placeholder="Enter movie title"
  style="box-sizing: border-box; max-width: calc(100% - 80px);"
/>

    <button on:click={searchMovie} class="bg-blue-500 hover:bg-blue-600 text-white p-3 rounded-r-lg transition-colors">
      Search
    </button>
  </div>
  {#if errorMessage}
    <div class="bg-red-100 border-l-4 border-red-500 text-red-700 p-4 mt-4 rounded" role="alert">
      <p class="font-bold">Error:</p>
      <p>{errorMessage}</p>
    </div>
  {/if}
  {#if movieData}
    <div class="mt-6">
      <h2 class="text-3xl font-semibold mb-4">{movieData.Title} ({movieData.Year})</h2>
      <div class="flex mb-4">
        <img class="w-1/3 rounded shadow-md mr-4" src={movieData.Poster} alt={movieData.Title} />
        <div>
          <p><strong>Director:</strong> {movieData.Director}</p>
          <p class="mt-2"><strong>Actors:</strong> {movieData.Actors}</p>
          <p class="mt-2 text-sm italic">{movieData.Plot}</p>
        </div>
      </div>
    </div>
  {/if}
</div>

<style>


</style>
