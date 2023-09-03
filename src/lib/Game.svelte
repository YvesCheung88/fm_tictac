<script lang="ts">
  import logo from "../assets/images/logo.svg";
  export let mode = "solo";

  let buttons = new Array(9).fill(null);
  let result = null as string | null;
  let turn = "X";

  const winCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  function setValue(i: number) {
    buttons[i] = turn;
    buttons = [...buttons];
    turn = turn == "X" ? "0" : "X";
    if (!buttons.includes(null)) {
      result = "Match Draw";
    } else {
      checkWinner();
    }
  }
  function checkWinner() {
    for (let i = 0; i < winCombinations.length; i++) {
      if (buttons[winCombinations[i][0]] != null) {
        if (
          buttons[winCombinations[i][0]] == buttons[winCombinations[i][1]] &&
          buttons[winCombinations[i][1]] == buttons[winCombinations[i][2]]
        ) {
          result = "Winner" + buttons[winCombinations[i][0]];
          break;
        }
      }
    }
  }

  function restart() {
    buttons = new Array(9).fill(null);
    result = null;
    turn = "X";
  }
</script>

<img src={logo} alt="logo" />
<p>mode: {mode}</p>
{#if !result}
  <div class="tictac">
    {#each buttons as button, i (i)}
      <button
        on:click={() => {
          setValue(i);
        }}
      >
        {button ? button : ""}
      </button>
    {/each}
  </div>
{:else}
  <div>
    {result}
    <button on:click={restart}> Restart </button>
  </div>
{/if}

<style>
  .tictac {
    width: 300px;
    height: 300 px;
    display: flex;
    flex-wrap: wrap;
  }
  .tictac button {
    width: 100px;
    height: 100 px;
    margin: 0px;
  }
</style>
