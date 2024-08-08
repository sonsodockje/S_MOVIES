<script>
  import { data } from "./lib/movies";
  import Navbar from "./lib/components/Navbar.svelte";
  import Modal from "./lib/components/Modal.svelte";

  const handleLike = (i) => {
    data[i].likeCount += 1;
    console.log(i);
  };
  let isModal = false;
  const handleModal = () => {
    isModal = !isModal;
  };
  let selectMovie = 0;
</script>

<Navbar />
<main class="container">
  <h1>영화정보</h1>

  {#each data as item, i}
    <div class="item">
      <figure>
        <img src="{item.imgUrl}" alt="{item.title}" />
      </figure>
      <div class="info">
        <h3 class="bg-yellow">{item.title}</h3>
        <p>개봉 : {item.year}</p>
        <p>장르 : {item.category}</p>
        <button
          on:click="{() => {
            handleLike(i);
          }}">좋아요 {item.likeCount}</button
        >
        <button
          class="detail"
          on:click="{() => {
            isModal = !isModal;
            selectMovie = i;
            console.log(selectMovie);
          }}">상세 정보</button
        >
      </div>
    </div>
  {/each}
</main>

{#if isModal}
  <Modal
    data="{data}"
    selectMovie="{selectMovie}"
    handleModal="{handleModal}"
  />
{/if}

<style>
  .item {
    display: flex;
    width: 100%;
    border: 1px solid #ccc;
    margin-bottom: 20px;
    padding: 1rem;
  }
  .item figure {
    width: 30%;
    margin-right: 1rem;
  }
  .item img {
    width: 100%;
  }
  .item .info {
    width: 100%;
  }
  .bg-yellow {
    background: gold;
    padding: 10px;
    color: #333;
  }
  .detail {
    background-color: rgb(41, 41, 197);
    color: #fff;
  }
</style>
