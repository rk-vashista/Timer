<script>
  import { onMount, afterUpdate } from 'svelte';
  import { flip } from 'svelte/animate';
  import { cubicOut } from 'svelte/easing';

  export let time;

  let hours, minutes, seconds;
  let prevTime = {};

  $: ({ hours, minutes, seconds } = time);

  function formatNumber(num) {
    return num.toString().padStart(2, '0');
  }

  function getDigits(value) {
    return formatNumber(value).split('');
  }

  onMount(() => {
    prevTime = { ...time };
  });

  afterUpdate(() => {
    prevTime = { ...time };
  });
</script>

<div class="flex gap-2 text-5xl md:text-6xl font-mono">
  {#each ['hours', 'minutes', 'seconds'] as unit}
    <div class="flex">
      {#each getDigits(time[unit]) as digit, i (unit + i)}
        <div 
          class="relative w-12 h-16 md:w-14 md:h-20 bg-gray-100 rounded-lg overflow-hidden shadow-inner"
          animate:flip={{ duration: 300, easing: cubicOut }}
        >
          <div class="absolute inset-0 flex items-center justify-center bg-white">
            {digit}
          </div>
        </div>
      {/each}
    </div>
    {#if unit !== 'seconds'}
      <div class="flex items-center text-3xl px-1 text-gray-400">:</div>
    {/if}
  {/each}
</div>