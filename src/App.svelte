<script lang="ts">
  import Game from "./lib/Game.svelte";
  import Menu from "./lib/Menu.svelte";

  let currentPage = "menu";
  function startSolo() {
    currentPage = "gameSolo";
  }
  function startDuo() {
    currentPage = "gameDuo";
  }
  function stop() {
    currentPage = "menu";
  }
</script>

{#if currentPage === "menu"}
  <Menu />
  <button on:click={startSolo}> Start-solo </button>
  <button on:click={startDuo}> Start-duo</button>
{/if}
{#if currentPage === "gameSolo"}
  <Game mode="solo" />
  <button on:click={stop}> Stop </button>
{/if}
{#if currentPage === "gameDuo"}
  <Game mode="duo" />
  <button on:click={stop}> Stop </button>
{/if}
