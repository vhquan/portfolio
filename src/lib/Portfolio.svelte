<script>
    import { onMount } from "svelte";
    let portfolio = [
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
        "worldcoin-wld",
    ];

    let API_URL = `https://api.coingecko.com/api/v3/coins/markets?ids=${portfolio.join(",")}&vs_currency=usd&price_change_percentage=30d&order=volume_desc`;

    let portfolioData = [];

    onMount(async () => {
        const response = await fetch(API_URL);
        const data = await response.json();
        if (data.length > 0) {
            portfolioData = data.map((crypto) => ({
                ...crypto,
                current_price: crypto.current_price,
                price_change_percentage_24h: crypto.price_change_percentage_24h,
                image: crypto.image.replace("large", "thumb"), // Replace 'large' with 'thumb' in the image URL
                symbol: crypto.symbol.toUpperCase(), // Uppercase the symbol
            }));
        }
    });
</script>

<div style="border: 2px solid black; border-style: solid; border-width: 2px;">
    <h3>Buy the f* dip</h3>
</div>

<table style="width:100%">
    <tr>
        <th style="text-align: left;">Name</th>
        <!-- Merged column with left alignment -->
        <th>Value</th>
        <th>Change (24h)</th>
    </tr>
    {#each portfolioData as crypto}
        <tr>
            <td style="text-align: left; vertical-align: middle;"
                ><img
                    src={crypto.image}
                    alt={crypto.symbol}
                    style="margin-right: 10px; vertical-align: middle;"
                />{crypto.symbol}</td
            >
            <!-- Merged column with image before text and left alignment -->
            <td style="text-align: right; vertical-align: middle;"
                >{Number.isFinite(crypto.current_price)
                    ? Number.isInteger(crypto.current_price)
                        ? crypto.current_price
                        : crypto.current_price.toFixed(4).replace(/\.?0+$/, "")
                    : crypto.current_price}</td
            >
            <td
                style="text-align: right; vertical-align: middle;"
                class={crypto.price_change_percentage_24h < 0
                    ? "negative-change"
                    : "positive-change"}
                >{crypto.price_change_percentage_24h.toFixed(2)}%</td
            >
        </tr>
    {/each}
</table>

<style>
    .negative-change {
        color: red;
    }
    .positive-change {
        color: green;
    }
</style>
