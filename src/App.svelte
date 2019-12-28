<script>
	let length = 6;
	let copied = false;

	const randLetter = () => String.fromCharCode(Math.floor(Math.random() * 26) + 65);
	const randNumber = () => (Math.floor(Math.random() * 10)).toString();
	const randomSymbol = () => '~!@_#$%^:*+&`|'.split('')[Math.floor(Math.random() * 14)];
	const randoms = [randLetter, randNumber, randomSymbol];

	const copyPass = () => {
		const copyText = document.querySelector('#password');
		const range = document.createRange();
		range.selectNode(copyText);
		window.getSelection().addRange(range);
		document.execCommand('copy');
		window.getSelection().removeAllRanges();
		copied = true;
		setTimeout(() => copied = false, 2000)
	};

	const generate = l => {
		let pass = '';
		for (let i = 0; i < l; i++) {
			pass += randoms[Math.floor(Math.random() * randoms.length)]()
		}
		return pass;
	};

 	$: password = generate(length);
</script>

<main>
	<h1>Password Generator</h1>
	<div class="generator-input">
		<p>Length: {length}</p>
		<label for="length">Set the length</label>
		<input bind:value={length} on:change={generate} min="6" max="50" id="length" type="range">

		<p id="password">{password}</p>
		<button on:click={copyPass}>Copy</button>
		{#if copied} <p>Copied!</p> {/if}
	</div>
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;

	}
	.generator-input {
		max-width: 960px;
		width: 100%;
		margin: auto;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>