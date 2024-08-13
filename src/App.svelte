<script>
  import { data } from "./lib/movies";
  import Navbar from "./lib/components/Navbar.svelte";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";

  let alertText = "";
  let selectMovie = 0;

  let data_temp = [...data];

  const handleLike = (id) => {
    // 원본 데이터 없데이트
    data.map((item) => {
      if (item.id === id) {
        item.likeCount += 1;
      }
    });
    console.log("data", data);
    console.log("temp", data_temp);

    // 현재 화면에 보여지는 것만 초기화
    data_temp ==
      data.filter((item) => {
        return data_temp.includes(item);
      });
  };

  let isModal = false;
  const handleModal = () => {
    isModal = !isModal;
  };
  const handleMovieNumber = (id) => {
    selectMovie = id;
  };

  let isEvent = true;
</script>

<Navbar />

{#if isEvent}
  <Event bind:isEvent="{isEvent}" />
{/if}

<SearchBar
  data="{data}"
  bind:data_temp="{data_temp}"
  bind:alertText="{alertText}"
/>

<button
  on:click="{() => {
    data_temp = [...data];
    alertText = '';
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
