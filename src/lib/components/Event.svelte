<script>
  import { fade } from "svelte/transition";
  export let isEvent = true;
  export let eventText;
  export let eventIndex;
</script>

<div class="event show" out:fade="{{ duration: 500 }}">
  <p>{eventText[eventIndex]}</p>
  <button
    on:click="{() => {
      isEvent = false;
    }}">X</button
  >
</div>

<!-- markup (zero or more items) goes here -->

<style>
  .event {
    width: 100%;
    background: #666;
    padding: 5px 1em;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #fff;
    text-align: left;
    margin-bottom: 0.2em;
    padding: 10px 20px;

    max-height: 0;
    opacity: 0;
    overflow: hidden;
    transition: all 0.4s;
  }

  .show {
    opacity: 1;
    max-height: 100px;
  }

  .event button {
    padding: 2px 5px;
  }

  .event p,
  .event button {
    margin: 0;
  }

  .event p {
    width: 100%;
  }
</style>
