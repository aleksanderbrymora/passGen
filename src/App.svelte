<script>
	let length = 6;
	let password = '';
	const randLetter = () => String.fromCharCode(Math.floor(Math.random() * 26) + 65);
	const randNumber = () => (Math.floor(Math.random() * 10)).toString();
	const randomSymbol = () => '~!@_#$%^:*+&`|'.split('')[Math.floor(Math.random() * 14)];
	const randoms = [randLetter, randNumber, randomSymbol];
	const generate = () => {
		let pass = '';
		for (let i = 0; i < length; i++) {
			pass += randoms[Math.floor(Math.random() * randoms.length)]()
		}
		password = pass;
	};
</script>

<main>
	<h1>Password Generator</h1>
	<div class="generator-input">
		<p>Length: {length}</p>
		<label for="length">Set the length</label>
		<input bind:value={length} on:change={generate} min="6" max="50" id="length" type="range">

		<p>{password}</p>
	</div>
</main>

<style>

</style>