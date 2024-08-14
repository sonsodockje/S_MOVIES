<script>
  import { data } from "./lib/movies";
  import Navbar from "./lib/components/Navbar.svelte";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";
  import { onDestroy, onMount } from "svelte";

  const eventText = ["홍보0", "홍보1", "홍보2"];
  let eventIndex = 0;

  let alertText = "";
  let selectMovie = 0;

  let data_temp = [...data];
  let intervalText;

  $: {
    clearInterval(intervalText);

    intervalText = setInterval(() => {
      if (eventText.length <= eventIndex + 1) {
        eventIndex = 0;
      } else {
        eventIndex += 1;
      }
    }, 1000);
  }

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
    data_temp = data.filter((item) => {
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
  <Event
    bind:isEvent="{isEvent}"
    eventText="{eventText}"
    eventIndex="{eventIndex}"
  />
{/if}

<SearchBar
  data="{data}"
  bind:data_temp="{data_temp}"
  bind:alertText="{alertText}"
/>
<div class="container">
  <button
    class="all"
    on:click="{() => {
      data_temp = [...data];
      alertText = '';
    }}">전체보기</button
  >
</div>
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
  .container {
    text-align: center;
  }
</style>
