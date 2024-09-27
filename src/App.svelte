<script>
  import { onMount } from 'svelte';

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
  let API_URL = `https://api.coingecko.com/api/v3/coins/markets?ids=${cryptoIds.join(',')}&vs_currency=usd`;
  let portfolioData = [];

  onMount(async () => {
    const response = await fetch(API_URL);
    const data = await response.json();
    if (data.length > 0) {
      portfolioData = data;
    }
  });
</script>

<main>
  <ul style="list-style-type: none; text-align: left;">
    <li style="display: flex; justify-content: space-between; font-weight: bold;">Name <span style="text-align: right;">Value</span></li>
    <hr style="border-bottom: 2px solid black;">
    {#each portfolioData as crypto}
      <li style="display: flex; justify-content: space-between;">{crypto.symbol} <span style="text-align: right;">{crypto.current_price}</span></li>
      <hr>
    {/each}
  </ul>

</main>

<style>
  main {
    padding: 1rem;
  }
</style>
