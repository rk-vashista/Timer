<script>
  export let mode;
  export let setTimer;

  const modes = [
    { id: 'pomodoro', label: 'Pomodoro' },
    { id: 'shortBreak', label: 'Short Break' },
    { id: 'longBreak', label: 'Long Break' }
  ];
</script>

<div class="flex gap-2 bg-gray-100 p-1 rounded-full">
  {#each modes as { id, label }}
    <button
      class="px-4 py-2 rounded-full transition-all duration-300 ease-in-out text-sm {mode === id ? 'bg-white text-gray-800 shadow-md' : 'text-gray-600 hover:bg-gray-200'}"
      on:click={() => setTimer(id)}
    >
      {label}
    </button>
  {/each}
</div>

