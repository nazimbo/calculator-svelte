<script lang="ts">
  const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
  const operators = ["/", "*", "-", "+", "="];

  let selectedOperator = "";
  let displayValue = "";
  let firstNumber = "";
  let secondNumber = "";

  const handleOperatorClick = (operator: string) => {
    if (!firstNumber) return;
    if (operator === "=") {
      if (secondNumber === "") return;
      displayValue = eval(`${firstNumber} ${selectedOperator} ${secondNumber}`);
      firstNumber = displayValue;
      secondNumber = "";
    }

    selectedOperator = operator;
  };

  const handleDecimal = (number: string, currentNumber: string) => {
    if (currentNumber === "" && number === ".") {
      return "0.";
    }
    return currentNumber + number;
  };

  const handleNumberClick = (number: string) => {
    if (displayValue === "" && number === "0") return;
    if (number === "." && displayValue.includes(".")) return;

    if (!selectedOperator) {
      firstNumber = handleDecimal(number, firstNumber);
    } else {
      secondNumber = handleDecimal(number, secondNumber);
    }

    displayValue = !selectedOperator ? firstNumber : secondNumber;
  };

  const handleClear = () => {
    displayValue = "";
    firstNumber = "";
    secondNumber = "";
    selectedOperator = "";
  };
</script>

<main>
  <div class="calculator">
    <div class="result">
      <h1>{displayValue}</h1>
    </div>
    <div class="buttons">
      <div class="numbers">
        {#each numbers as number (number)}
          <button on:click={() => handleNumberClick(number)}>
            {number}
          </button>
        {/each}
        <button on:click={handleClear}> C </button>
      </div>

      <div class="operators">
        {#each operators as operator (operator)}
          <button class={`${operator === selectedOperator ? "button-clicked" : ""}`} on:click={() => handleOperatorClick(operator)}>
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

  .operators .button-clicked {
    background-color: #c0c0c0;
  }
</style>
