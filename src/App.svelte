<script>
  import { data } from "./lib/movies";
  import Navbar from "./lib/components/Navbar.svelte";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";

  let data_temp = [...data];
  let selectMovie = 0;

  const handleLike = (i) => {
    data[i].likeCount += 1;
    console.log(i);
    console.log(data_temp);
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

<SearchBar data="{data}" bind:data_temp="{data_temp}" />

<button
  on:click="{() => {
    data_temp = [...data];
  }}">전체보기</button
>

<Movies
  data_temp="{data_temp}"
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
