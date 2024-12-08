<script>
  import svelteLogo from './assets/svelte.svg';
  import { onMount } from 'svelte';

  let name = '';
  let response = '';
  let spin = false;

  const sayHello = async () => {
    response = name ? `Hello, ${name}!` : 'Please enter your name.';
  };

  onMount(() => {
    spin = true; // Trigger the spin animation when the component mounts
    updateTime(); // Start clock on mount
    clockInterval = setInterval(updateTime, 1000); // Update clock every second
  });

  // Cleanup interval on component destruction
  let clockInterval;
  onDestroy(() => {
    clearInterval(clockInterval);
  });

  // Clock functionality
  let time = new Date();
  const updateTime = () => {
    const localTime = new Date();
    const nycOffset = -5; // UTC-5 for New York City
    const utc = localTime.getTime() + localTime.getTimezoneOffset() * 60000;
    time = new Date(utc + nycOffset * 3600000);
  };

  const handleClick = (buttonName) => {
    alert(`${buttonName} button clicked!`);
  };
</script>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }

  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }

  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #61dafbaa);
  }

  @keyframes logo-spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  .spin {
    animation: logo-spin infinite 20s linear;
  }

  .card {
    padding: 2em;
  }

  .read-the-docs {
    color: #888;
  }

  .input-box {
    width: 25%;
    border-radius: 5px;
    border: 2px solid #888;
    padding: 10px;
  }

  .red-button {
    background-color: red;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 5px;
  }

  .red-button:hover {
    background-color: darkred;
  }

  .button {
    background-color: lightgray;
    color: black;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 5px;
    margin-left: 10px;
  }

  .button:hover {
    background-color: gray;
  }

  .clock {
    font-family: "Arial", sans-serif;
    font-size: 1.5rem;
    color: #333;
    text-align: center;
    margin: 20px 0;
  }

  .clock span {
    animation: pulse 1s infinite;
  }

  @keyframes pulse {
    0%, 100% {
      transform: scale(1);
    }
    50% {
      transform: scale(1.1);
    }
  }
</style>

<main>
  <div>
    <a href="https://svelte.dev/" target="_blank">
      <img src={svelteLogo} class="logo svelte" alt="Svelte.js logo" class:spin={spin} />
    </a>

    <h1>Genezio + Svelte = ❤️</h1>

    <div class="card">
      <input
        type="text"
        class="input-box"
        bind:value={name}
        placeholder="Enter your name"
      />
      <br />
      <br />
      <button on:click={sayHello}>Say Hello</button>
      <p class="read-the-docs">{response}</p>
    </div>

    <div class="clock">
      <span>{time.toLocaleTimeString('en-US', { timeZone: 'America/New_York' })}</span>
    </div>

    <div>
      <button class="red-button" on:click={() => handleClick('Red')}>Red Button</button>
      <button class="button" on:click={() => handleClick('Default')}>Default Button</button>
    </div>
  </div>
</main>
