<script>
  export let data = [];
  export let isModal = false;
  export let selectMovie = 0;
  export let handleLike;
  export let handleMovieNumber;
</script>

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
            handleMovieNumber(i);
          }}">상세 정보</button
        >
      </div>
    </div>
  {/each}
</main>

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
    background: rgb(255, 171, 240);
    padding: 10px;
    color: #333;
  }
  .detail {
    background-color: rgb(41, 41, 197);
    color: #fff;
  }
</style>
