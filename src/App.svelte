<script>
  import { data } from "./lib/movies";
  import Navbar from "./lib/components/Navbar.svelte";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";

  let selectMovie = 0;
  const handleLike = (i) => {
    data[i].likeCount += 1;
  };

  let isModal = false;
  const handleModal = () => {
    isModal = !isModal;
  };
  const handleMovieNumber = (i) => {
    selectMovie = i;
  };

  let isEvent = true;
</script>

<Navbar />

{#if isEvent}
  <Event bind:isEvent="{isEvent}" />
{/if}

<SearchBar />

<Movies
  data="{data}"
  bind:isModal="{isModal}"
  handleMovieNumber="{handleMovieNumber}"
  handleLike="{handleLike}"
/>

{#if isModal}
  <Modal
    data="{data}"
    selectMovie="{selectMovie}"
    handleModal="{handleModal}"
  />
{/if}

<style>
</style>
