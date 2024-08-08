<script>
  export let data;
  export let selectMovie;
  export let handleModal;
</script>

<div class="modal">
  <div class="inner">
    <h3>{data[selectMovie].title}</h3>
    <p>{@html data[selectMovie].story}</p>
    <button on:click="{handleModal}">닫기</button>
  </div>
</div>

<style>
  .modal {
    background: rgba(0, 0, 0, 0.7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal .inner {
    background: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
  }
</style>
