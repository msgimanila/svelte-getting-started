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

  // Fetch 5 random products from a free image site (Pixabay)
  onMount(async () => {
    // Example: Here using static image URLs for simplicity
    products = [
      { id: 1, name: 'Product 1', imageUrl: 'https://cdn.pixabay.com/photo/2017/08/30/01/01/ball-2692535_960_720.jpg' },
      { id: 2, name: 'Product 2', imageUrl: 'https://cdn.pixabay.com/photo/2017/08/30/01/01/ball-2692535_960_720.jpg' },
      { id: 3, name: 'Product 3', imageUrl: 'https://cdn.pixabay.com/photo/2017/08/30/01/01/ball-2692535_960_720.jpg' },
      { id: 4, name: 'Product 4', imageUrl: 'https://cdn.pixabay.com/photo/2017/08/30/01/01/ball-2692535_960_720.jpg' },
      { id: 5, name: 'Product 5', imageUrl: 'https://cdn.pixabay.com/photo/2017/08/30/01/01/ball-2692535_960_720.jpg' }
    ];
  });

  // Add product to cart
  function addToCart(product) {
    cart = [...cart, product];
  }
</script>

<style>
  .product-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
  }

  .product {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    background-color: #fff;
  }

  .product img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
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
