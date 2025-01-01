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

<div class="flex gap-2 text-6xl md:text-8xl font-mono">
  {#each ['hours', 'minutes', 'seconds'] as unit}
    <div class="flex">
      {#each getDigits(time[unit]) as digit, i (unit + i)}
        <div 
          class="relative w-16 h-24 md:w-24 md:h-32 bg-gray-800 rounded-lg overflow-hidden"
          animate:flip={{ duration: 300, easing: cubicOut }}
        >
          <div class="absolute inset-0 flex items-center justify-center">
            {digit}
          </div>
        </div>
      {/each}
    </div>
    {#if unit !== 'seconds'}
      <div class="flex items-center text-4xl px-2">:</div>
    {/if}
  {/each}
</div>