<script>
	import axios from "axios"
	import { spring } from "svelte/motion";
	let address = '';
	let NFTs = 0;

	const fadeSpring = spring(1, { stiffness: 0.1, damping: 0.5 });
  const transformSpring = spring(0, { stiffness: 0.2, damping: 0.1 });

  const toggleFade = () => fadeSpring.update(val => (val ? 0 : 1));
  const toggleTransform = () => transformSpring.update(val => (val ? 0 : 500));
  const snapTransform = () => transformSpring.update(val => val, { hard: true });

	async function getWalletBalance() {
		balance = (await axios.get(`hitt://localhost: 3001/get_wallet_balance/${address}`)
	).data.balance;
	}

	async function getNFTs() {
		NFTs = (await axios.get(`LINK`)
		).data.NFTs
	}
</script>


<div style="opacity: {$fadeSpring}">Little bit about me. I am Alumist and thats all folks.</div>
<br />

<div class="buttonFade"on:click={toggleFade}>Click Me!</div>


<hr />


<div class="container">
	<div class="text"> 
		{NFTs}
	</div>

<div class="button">
	connect wallet</div>

<div class="text"> 
	NFTs You have: {NFTs} NFTs
	</div>
</div>

<style>
	.buttonFade {
		background-color: aquamarine;
		display: flex;
		flex-direction: column;
		align-items: center;
		font-size: 2em;
		justify-content: center;
		background-position: 1em;
		padding: 0.1em 0.4em;
		background-size: 0%;
	}
	.container {
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.textbox {
		font-size: 1.2em;
	}

	.button {
		background-color: black;
		padding: 0.4em 0.8em;
		color: white;
		font-size: 1.2em;
		margin: 1em 0;
		cursor: pointer;
		transition-duration: 0.3s;
	}
	.button:hover {
		background-color: aqua;
	}

	.text {
		font-size: 1.4em;
		font-weight: bold;
	}
</style>
