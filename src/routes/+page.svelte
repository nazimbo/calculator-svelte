<script lang="ts">
  const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", ".", "C"];
  const operators = ["/", "*", "-", "+", "="];

  let selectedOperator = "";

  const handleOperatorClick = (operator: string) => {
    selectedOperator = operator;
  };
</script>

<main>
  <div class="calculator">
    <div class="result"><h1 style="color: blue;">{selectedOperator}</h1></div>
    <div class="buttons">
      <div class="numbers">
        {#each numbers as number (number)}
          <button>
            {number}
          </button>
        {/each}
      </div>

      <div class="operators">
        {#each operators as operator (operator)}
          <button on:click={() => handleOperatorClick(operator)}>
            {operator}
          </button>
        {/each}
      </div>
    </div>
  </div>
</main>

<style>
  main {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .calculator {
    width: 400px;
    height: 600px;
    background-color: #f3f3f3;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .result {
    width: 100%;
    height: 20%;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 0 20px;
    font-size: 2em;
  }

  .buttons {
    width: 100%;
    height: 80%;
    display: flex;
  }

  .numbers {
    width: 75%;
    height: 100%;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(4, 1fr);
  }

  .numbers button {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    border: none;
    background-color: #fff;
    cursor: pointer;
  }

  .numbers button:hover {
    background-color: #e0e0e0;
  }

  .operators {
    width: 25%;
    height: 100%;
    display: flex;
    flex-direction: column;
  }

  .operators button {
    width: 100%;
    height: 20%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    border: none;
    background-color: #f3f3f3;
    cursor: pointer;
  }

  .operators button:hover {
    background-color: #e0e0e0;
  }
</style>
