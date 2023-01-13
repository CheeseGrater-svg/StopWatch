<script lang="ts">
	import icon from '$lib/assets/stopwatch.png';

	enum STATE {
		NEW,
		RUNNING,
		PAUSED
	}

	let state: STATE = STATE.NEW;
	let startTime: number = 0;
	let elapsedTime: number = 0;
	let oldElapsedTime: number = 0;
	let interval: number;

	$: ms = String(elapsedTime % 1000)
		.slice(-3, -1)
		.padStart(2, '0');
	$: s = String(Math.floor(elapsedTime / 1000) % 60)
		.slice(-2)
		.padStart(2, '0');
	$: m = String(Math.floor(elapsedTime / 1000 / 60) % 60)
		.slice(-2)
		.padStart(2, '0');
	$: h = String(Math.floor(elapsedTime / 1000 / 60 / 60) % 60)
		.slice(-2)
		.padStart(2, '0');

	const start = () => {
		startTime = Date.now();
		state = STATE.RUNNING;
		interval = Number(
			setInterval(() => {
				if (state === STATE.RUNNING) {
					const endTime = Date.now();
					elapsedTime = endTime - startTime + oldElapsedTime;
				}
			})
		);
	};

	const reset = () => {
		elapsedTime = 0;
		oldElapsedTime = 0;
		state = STATE.NEW;
		clearInterval(interval);
	};

	const stop = () => {
		state = STATE.PAUSED;
		oldElapsedTime = elapsedTime;
	};

	const resume = () => {
		startTime = Date.now();
		state = STATE.RUNNING;
	};
</script>

<div class="relative mt-16">
	<img src={icon} alt="watch icon" class="peer relative z-10 box-content w-24 p-2" />
	<div
		class="absolute inset-0 z-0 rounded-3xl bg-gradient-to-r from-cyan-500 to-fuchsia-500 opacity-50 blur-xl"
	/>
</div>

<h1 class="mt-6 text-5xl font-black leading-none">StopWatch</h1>
<h2 class="text-base font-medium leading-relaxed">Coolest Web Stopwatch</h2>

<div class="relative mt-16">
	{#if state === STATE.NEW}
		<button
			class="peer relative z-10 w-40 rounded-lg border border-white bg-white py-1 text-base font-bold leading-relaxed text-black transition hover:bg-black hover:text-white"
			on:click={start}>Start</button
		>
	{/if}
	{#if state === STATE.RUNNING}
		<button
			class="peer relative z-10 w-40 rounded-lg border border-white bg-white py-1 text-base font-bold leading-relaxed text-black transition hover:bg-black hover:text-white"
			on:click={stop}>Stop</button
		>
	{/if}
	{#if state === STATE.PAUSED}
		<button
			class="peer relative z-10 w-40 rounded-lg border border-white bg-white py-1 text-base font-bold leading-relaxed text-black transition hover:bg-black hover:text-white"
			on:click={resume}>Start</button
		>
	{/if}
	<div
		class="absolute inset-0 z-0 rounded-3xl bg-gradient-to-r from-cyan-500 to-fuchsia-500 opacity-75 blur-xl"
	/>
</div>

<div class="mt-8 flex w-3/4 max-w-sm justify-between md:min-w-[720px] md:max-w-screen-md">
	<div class="flex flex-col items-center">
		<div
			class="flex h-16 w-14 items-center justify-center rounded-lg border border-neutral-700 p-2 md:h-44 md:w-48 md:p-0"
		>
			<h1 class="text-3xl font-black md:text-9xl">{h}</h1>
		</div>
		<h2 class="text-base font-medium leading-relaxed">H</h2>
	</div>
	<div class="flex flex-col items-center">
		<div
			class="flex h-16 w-14 items-center justify-center rounded-lg border border-neutral-700 p-2 md:h-44 md:w-48 md:p-0"
		>
			<h1 class="text-3xl font-black md:text-9xl">{m}</h1>
		</div>
		<h2 class="text-base font-medium leading-relaxed">M</h2>
	</div>
	<div class="flex flex-col items-center">
		<div
			class="flex h-16 w-14 items-center justify-center rounded-lg border border-neutral-700 p-2 md:h-44 md:w-48 md:p-0"
		>
			<h1 class="text-3xl font-black md:text-9xl">{s}</h1>
		</div>
		<h2 class="text-base font-medium leading-relaxed">S</h2>
	</div>
	<div class="flex flex-col items-center">
		<div
			class="box-border flex h-16 w-14 items-center justify-center rounded-lg border border-neutral-700 p-2 md:h-44 md:w-32 md:items-end md:p-0"
		>
			<h1 class="text-3xl font-black md:pb-7 md:text-7xl">{ms}</h1>
		</div>
		<h2 class="text-base font-medium leading-relaxed">MS</h2>
	</div>
</div>

{#if state === STATE.RUNNING || state === STATE.PAUSED}
	<button
		class="mt-8 w-40 rounded-lg border border-neutral-700 bg-black py-1 text-base font-bold leading-relaxed text-neutral-700 transition hover:border-white hover:text-white"
		on:click={reset}>Reset</button
	>
{/if}

<p class="mt-24 mb-12 text-center text-sm font-normal">
	© 2023 IncogNEET<br />
	<a href="https://github.com/IncogNEET/StopWatch" class="text-blue-500 hover:underline">GitHub</a>
	| <a href="/colophon" class="text-blue-500 hover:underline">Colophon</a>
</p>
