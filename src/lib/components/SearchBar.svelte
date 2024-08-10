<script>
  let inputText = "";
  let alertText = "";

  export let data = [];

  $: if (inputText.length > 16) {
    alertText = "입력 한도 초과";
  } else {
    alertText = "";
  }

  const serchMovie = () => {
    let findeMovie = data.filter((movie) => {
      return movie.title == inputText;
    });
    console.log(findeMovie);

    if (findeMovie.length === 0) {
      alertText = "검색 결과가 없습니다.";
    } else {
      alertText = "";
    }
  };
</script>

<div class="search-box">
  <div class="input-group">
    <input
      type="text"
      bind:value="{inputText}"
      on:keydown="{(e) => {
        if (e.key === 'Enter') {
          serchMovie();
        }
      }}"
    />
    <button on:click="{serchMovie}">검색</button>
  </div>
</div>

{#if alertText}
  <p class="text-center alert">{alertText}</p>
{/if}

<style>
  .search-box {
    padding: 0 20px;
    margin-top: 20px;
  }

  .input-group {
    width: 100%;
    border: 1px solid #ccc;
    position: relative;
    padding: 0 20px;
  }

  .search-box input {
    width: 100%;
    border: none;
    outline: none;
    padding: 10px;
  }

  .search-box button {
    position: absolute;
    right: 0;
    top: 0;
    border: none;
    outline: none;
    background: #666;
    color: #fff;
    width: 5em;
    height: 100%;
    margin: 0;
    padding: 0;
    border-radius: 0;
  }

  .text-center {
    text-align: center;
  }

  .alert {
    color: red;
  }
</style>
