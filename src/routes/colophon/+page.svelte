<script>
	import icon from '$lib/assets/stopwatch.png';
	import soyjacks from '$lib/assets/sveltesoyjacks.png';
</script>

<a href="../">
	<div class="relative mt-16">
		<img src={icon} alt="watch icon" class="h- peer relative z-10 box-content h-[84px] w-24 p-2" />
		<div
			class="absolute inset-0 z-0 rounded-3xl bg-gradient-to-r from-cyan-500 to-fuchsia-500 opacity-50 blur-xl"
		/>
	</div>
</a>

<a href="../"><h1 class="mt-6 text-5xl font-black leading-none">StopWatch</h1></a>
<h2 class="text-base font-medium leading-relaxed">Colophon</h2>

<section class="mt-12 w-3/4 text-sm font-normal leading-relaxed text-neutral-500 sm:max-w-md">
	<p>This website was designed and developed by IncogNEET in Japan.</p>
	<p class="mt-4">
		It is built using <a href="https://code.visualstudio.com" class="text-blue-500 hover:underline"
			>VS Code</a
		>
		with <a href="https://kit.svelte.dev" class="text-blue-500 hover:underline">SvelteKit</a> as the
		framework and
		<a href="https://tailwindcss.com" class="text-blue-500 hover:underline">TailwindCSS</a>
		as the front end, and deployed using
		<a href="https://vercel.com" class="text-blue-500 hover:underline">Vercel</a>.
	</p>
	<p class="mt-4">
		It is designed in <a href="https://www.figma.com" class="text-blue-500 hover:underline">Figma</a
		>
		and the type is set in
		<a href="https://fonts.google.com/specimen/Inter" class="text-blue-500 hover:underline"
			>Inter by Rasmus Andersson</a
		>.
	</p>
	<p class="mt-4">
		The source code can be found in this <a
			href="https://github.com/IncogNEET/StopWatch"
			class="text-blue-500 hover:underline">GitHub repository</a
		>.
	</p>
</section>

<p class="mt-24">Thanks for visiting!</p>
<div class="relative mt-4">
	<img src={soyjacks} alt="two soyjacks pointing svelte" class="relative z-10 w-56 rounded-xl" />
	<div
		class="absolute inset-0 z-0 rounded-3xl bg-gradient-to-r from-cyan-500 to-fuchsia-500 opacity-75 blur-xl"
	/>
</div>
<p class="mt-4 mb-12">❤️</p>
