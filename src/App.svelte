<script>
  import { onMount } from 'svelte';
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'

  let cryptoIds = [
    "automata",
    "bitcoin",
    "cartesi",
    "chainlink",
    "endurance",
    "ethereum",
    "filecoin",
    "flow",
    "frax-share",
    "hifi-finance",
    "hooked-protocol",
    "icon",
    "iostoken",
    "iota",
    "manta-network",
    "memecoin-2",
    "orchid-protocol",
    "polkadot",
    "radiant-capital",
    "rif-token",
    "syscoin",
    "threshold-network-token",
    "worldcoin-wld"
  ];
  let API_URL = `https://api.coingecko.com/api/v3/simple/price?ids=${cryptoIds.join(',')}&vs_currencies=usd`;
  let portfolioData = {};

  onMount(async () => {
    const response = await fetch(API_URL);
    const data = await response.json();
    if (Object.keys(data).length > 0) {
      portfolioData = data;
    }
  });
</script>

<main>
  <div>
    <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  {#each Object.entries(portfolioData) as [crypto, { usd }]}
    <p>{crypto} -> {usd}</p>
  {/each}

</main>

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
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
</style>
