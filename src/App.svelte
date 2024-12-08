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
let currentDate = new Date();
  let selectedDate = null;
  let availableSlots = [];
  let bookedSlots = [];

  // Generate days for the current month
  let days = [];
  const generateCalendar = () => {
    days = [];
    const year = currentDate.getFullYear();
    const month = currentDate.getMonth();

    const firstDay = new Date(year, month, 1).getDay();
    const lastDate = new Date(year, month + 1, 0).getDate();

    // Fill leading empty spaces
    for (let i = 0; i < firstDay; i++) {
      days.push(null);
    }

    // Fill actual days
    for (let i = 1; i <= lastDate; i++) {
      days.push(new Date(year, month, i));
    }
  };

  const selectDate = (day) => {
    selectedDate = day;
    generateAvailableSlots();
  };

  const generateAvailableSlots = () => {
    if (selectedDate) {
      availableSlots = [
        "10:00 AM",
        "11:00 AM",
        "1:00 PM",
        "2:00 PM",
        "3:00 PM",
        "4:00 PM",
      ].filter((slot) => !bookedSlots.find((b) => b.date.toDateString() === selectedDate.toDateString() && b.slot === slot));
    }
  };

  const bookSlot = (slot) => {
    bookedSlots.push({ date: selectedDate, slot });
    generateAvailableSlots();
    alert(`Booked ${slot} on ${selectedDate.toDateString()}`);
  };

  const goToPreviousMonth = () => {
    currentDate = new Date(currentDate.getFullYear(), currentDate.getMonth() - 1, 1);
    generateCalendar();
  };

  const goToNextMonth = () => {
    currentDate = new Date(currentDate.getFullYear(), currentDate.getMonth() + 1, 1);
    generateCalendar();
  };

  onMount(generateCalendar);

let products = [];
  let cart = [];

  // Fetch 5 random products from a free image site (Pixabay) or use pre-defined product data
  onMount(async () => {
    // Replace with a real API call to fetch products if needed
    products = [
      { id: 1, name: 'Product 1', imageUrl: 'https://pixabay.com/get/57e0d741485baf14f1dc8460962e337b1c3d2e24e7e44f4e762d79ec974e_640.jpg' },
      { id: 2, name: 'Product 2', imageUrl: 'https://pixabay.com/get/57e0d741485baf14f1dc8460962e337b1c3d2e24e7e44f4e762d79ec974e_640.jpg' },
      { id: 3, name: 'Product 3', imageUrl: 'https://pixabay.com/get/57e0d741485baf14f1dc8460962e337b1c3d2e24e7e44f4e762d79ec974e_640.jpg' },
      { id: 4, name: 'Product 4', imageUrl: 'https://pixabay.com/get/57e0d741485baf14f1dc8460962e337b1c3d2e24e7e44f4e762d79ec974e_640.jpg' },
      { id: 5, name: 'Product 5', imageUrl: 'https://pixabay.com/get/57e0d741485baf14f1dc8460962e337b1c3d2e24e7e44f4e762d79ec974e_640.jpg' }
    ];
  });

  // Add product to cart
  function addToCart(product) {
    cart = [...cart, product];
  }
</script>
<style>
  /* Styling remains the same as before */
</style>
<style>
  .product-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
  }

  .product {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
  }

  .product img {
    max-width: 100%;
    height: auto;
  }

  .cart {
    margin-top: 20px;
    padding: 10px;
    background-color: #f4f4f4;
    border: 1px solid #ddd;
  }

  .button {
    padding: 10px 20px;
    margin-top: 10px;
    background-color: #4CAF50;
    color: white;
    border: none;
    cursor: pointer;
  }

  .button:hover {
    background-color: #45a049;
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


<style>
  .calendar {
    display: flex;
    flex-direction: column;
    align-items: center;
    font-family: Arial, sans-serif;
  }

  .calendar-header {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 10px 0;
  }

  .days-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 5px;
    width: 100%;
    margin-top: 10px;
  }

  .day {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
    background: #f0f0f0;
    border-radius: 4px;
    cursor: pointer;
  }

  .day.selected {
    background: #0077cc;
    color: white;
  }

  .day.disabled {
    background: #ccc;
    cursor: not-allowed;
  }

  .slots {
    margin-top: 20px;
  }

  .slot {
    margin: 5px 0;
    padding: 10px;
    background: #0077cc;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  .slot:hover {
    background: #005fa3;
  }
</style>

<div class="calendar">
  <div class="calendar-header">
    <button on:click={goToPreviousMonth}>&lt; Previous</button>
    <h2>{currentDate.toLocaleString('default', { month: 'long', year: 'numeric' })}</h2>
    <button on:click={goToNextMonth}>Next &gt;</button>
  </div>

  <div class="days-grid">
    <!-- Render day names -->
    {#each ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"] as dayName}
      <div class="day disabled">{dayName}</div>
    {/each}

    <!-- Render days -->
    {#each days as day, i}
      <div
        class="day {selectedDate && selectedDate.toDateString() === day?.toDateString() ? 'selected' : ''} {day ? '' : 'disabled'}"
        on:click={() => day && selectDate(day)}
      >
        {day ? day.getDate() : ''}
      </div>
    {/each}
  </div>

  {#if selectedDate}
    <div class="slots">
      <h3>Available Slots for {selectedDate.toDateString()}</h3>
      {#if availableSlots.length > 0}
        {#each availableSlots as slot}
          <button class="slot" on:click={() => bookSlot(slot)}>{slot}</button>
        {/each}
      {:else}
        <p>No slots available.</p>
      {/if}
    </div>
  {/if}
</div>
<h1>Product List</h1>

  <div class="product-list">
    {#each products as product}
      <div class="product">
        <img src={product.imageUrl} alt={product.name} />
        <h3>{product.name}</h3>
        <button class="button" on:click={() => addToCart(product)}>Add to Cart</button>
      </div>
    {/each}
  </div>

  <div class="cart">
    <h2>Cart</h2>
    {#if cart.length > 0}
      <ul>
        {#each cart as item}
          <li>{item.name}</li>
        {/each}
      </ul>
    {:else}
      <p>Your cart is empty.</p>
    {/if}
  </div>
</main>
