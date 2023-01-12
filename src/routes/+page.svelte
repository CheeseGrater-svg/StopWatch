<script lang="ts">
  import icon from "$lib/assets/stopwatch.png";

  enum STATE {
    NEW,
    RUNNING,
    PAUSED,
  }

  let state: STATE = STATE.NEW;
  let startTime: number = 0;
  let elapsedTime: number = 0;
  let oldElapsedTime: number = 0;
  let interval: number;

  $: ms = String(elapsedTime % 1000).slice(-3, -1).padStart(2, '0');
  $: s = String(Math.floor(elapsedTime / 1000) % 60).slice(-2).padStart(2, '0');
  $: m = String(Math.floor((elapsedTime / 1000) / 60) % 60).slice(-2).padStart(2, '0');
  $: h = String(Math.floor(((elapsedTime / 1000) / 60) / 60) % 60).slice(-2).padStart(2, '0');

  const start = () => {
    startTime = Date.now();
    state = STATE.RUNNING;
    interval = setInterval(() => {
      if (state === STATE.RUNNING) {
        const endTime = Date.now();
        elapsedTime = endTime - startTime + oldElapsedTime;
      }
    });
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
  <img src={icon} alt="watch icon" class="w-24 box-content relative p-2 peer z-10"/>
  <div class="absolute inset-0 z-0 bg-gradient-to-r from-cyan-500 to-fuchsia-500 rounded-3xl blur-xl opacity-50"></div>
</div>


<h1 class="text-5xl font-black leading-none mt-6">StopWatch</h1>
<h2 class="text-base font-medium leading-relaxed">Coolest Web Stopwatch</h2>

<div class="relative mt-16">
  {#if state === STATE.NEW}
  <button class="transition bg-white hover:bg-black hover:text-white text-black w-40 py-1 text-base leading-relaxed rounded-lg font-bold border border-white relative z-10 peer" on:click={start}>Start</button>
  {/if}
  {#if state === STATE.RUNNING}
  <button class="transition bg-white hover:bg-black hover:text-white text-black w-40 py-1 text-base leading-relaxed rounded-lg font-bold border border-white relative z-10 peer" on:click={stop}>Stop</button>
  {/if}
  {#if state === STATE.PAUSED}
  <button class="transition bg-white hover:bg-black hover:text-white text-black w-40 py-1 text-base leading-relaxed rounded-lg font-bold border border-white relative z-10 peer" on:click={resume}>Start</button>
  {/if}
  <div class="absolute inset-0 z-0 bg-gradient-to-r from-cyan-500 to-fuchsia-500 rounded-3xl blur-xl opacity-75"></div>
</div>

<div class="flex mt-8 w-3/4 max-w-sm md:max-w-screen-md md:min-w-[720px] justify-between">
  <div class="flex flex-col items-center">
    <div class="md:w-48 md:h-44 md:p-0 w-14 h-16 p-2 border border-neutral-700 rounded-lg flex items-center justify-center">
      <h1 class="md:text-9xl text-3xl font-black">{h}</h1>
    </div>
    <h2 class="text-base font-medium leading-relaxed">H</h2>
  </div>
  <div class="flex flex-col items-center">
    <div class="md:w-48 md:h-44 md:p-0 w-14 h-16 p-2 border border-neutral-700 rounded-lg flex items-center justify-center">
      <h1 class="md:text-9xl text-3xl font-black">{m}</h1>
    </div>
    <h2 class="text-base font-medium leading-relaxed">M</h2>
  </div>
  <div class="flex flex-col items-center">
    <div class="md:w-48 md:h-44 md:p-0 w-14 h-16 p-2 border border-neutral-700 rounded-lg flex items-center justify-center">
      <h1 class="md:text-9xl text-3xl font-black">{s}</h1>
    </div>
    <h2 class="text-base font-medium leading-relaxed">S</h2>
  </div>
  <div class="flex flex-col items-center">
    <div class="md:w-32 md:h-44 md:p-0 w-14 h-16 p-2 border border-neutral-700 rounded-lg flex box-border md:items-end items-center justify-center">
      <h1 class="md:text-7xl text-3xl font-black md:pb-7">{ms}</h1>
    </div>
    <h2 class="text-base font-medium leading-relaxed">MS</h2>
  </div>
</div>

{#if state === STATE.RUNNING || state === STATE.PAUSED}
<button class="transition mt-8 bg-black text-neutral-700 w-40 py-1 text-base leading-relaxed rounded-lg font-bold border border-neutral-700 hover:text-white hover:border-white" on:click={reset}>Reset</button>
{/if}

<p class="mt-24 text-sm font-normal text-center">© 2023 CheeseGrater<br/><a href="/colophon" class="text-blue-500 hover:underline">Colophon</a></p>
