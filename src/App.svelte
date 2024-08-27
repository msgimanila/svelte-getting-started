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
    <a href="https://genezio.com" target="_blank">
      <img
              src="https://raw.githubusercontent.com/Genez-io/graphics/main/svg/Logo_Genezio_White.svg"
              class="logo genezio light"
              alt="Genezio Logo"
      />
      <img
              src="https://raw.githubusercontent.com/Genez-io/graphics/main/svg/Logo_Genezio_Black.svg"
              class="logo genezio dark"
              alt="Genezio Logo"
      />
    </a>
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
</main>