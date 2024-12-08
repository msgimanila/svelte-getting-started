<script>
  import svelteLogo from './assets/svelte.svg';
  import { onMount, onDestroy } from 'svelte';

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
  /* Styling remains the same as before */
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
