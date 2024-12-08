<script>
  import svelteLogo from './assets/svelte.svg';
  import { onMount } from 'svelte';

  let name = '';
  let response = '';

  const sayHello = async () => {
    response = name ? `Hello, ${name}!` : 'Please enter your name.';
  };

  // Use a reactive variable to handle the animation class
  let spin = false;

  onMount(() => {
    spin = true; // Trigger the spin animation when the component mounts
  });
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

  @media (prefers-color-scheme: dark) {
    .dark {
      display: none; /* Hide light logo in dark mode */
    }
  }

  @media (prefers-color-scheme: light) {
    .light {
      display: none; /* Hide dark logo in light mode */
    }
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
    box-shadow: none !important;
    border: 2px solid #888;
    padding: 10px;
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
  </div>
<script>
  const handleClick = (buttonName) => {
    alert(`${buttonName} button clicked!`);
  };
</script>

<style>
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
</style>

<div>
  <button class="red-button" on:click={() => handleClick('Red')}>Red Button</button>
  <button class="button" on:click={() => handleClick('Default')}>Default Button</button>
</div>
<script>
  import { onMount } from "svelte";

  let time = new Date();

  const updateTime = () => {
    const localTime = new Date();
    const nycOffset = -5; // New York City is UTC-5
    const utc = localTime.getTime() + localTime.getTimezoneOffset() * 60000;
    time = new Date(utc + nycOffset * 3600000);
  };

  let interval;

  onMount(() => {
    updateTime();
    interval = setInterval(updateTime, 1000);

    return () => clearInterval(interval); // Cleanup on component destroy
  });
</script>

<style>
  .clock {
    font-family: "Arial", sans-serif;
    font-size: 2rem;
    color: #333;
    text-align: center;
    margin: 20px;
  }

  .digits {
    display: inline-block;
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

<div class="clock">
  <span class="digits">{time.toLocaleTimeString("en-US", { timeZone: "America/New_York" })}</span>
</div>

</main>
