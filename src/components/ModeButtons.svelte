<script>
    export let mode;
    export let setTimer;
  </script>
  
  <div class="flex gap-4">
    <button
      class="px-4 py-2 rounded-full {mode === 'pomodoro' ? 'bg-white text-black' : 'bg-transparent text-white border border-white/20'}"
      on:click={() => setTimer('pomodoro')}
    >
      pomodoro
    </button>
    <button
      class="px-4 py-2 rounded-full {mode === 'shortBreak' ? 'bg-white text-black' : 'bg-transparent text-white border border-white/20'}"
      on:click={() => setTimer('shortBreak')}
    >
      short break
    </button>
    <button
      class="px-4 py-2 rounded-full {mode === 'longBreak' ? 'bg-white text-black' : 'bg-transparent text-white border border-white/20'}"
      on:click={() => setTimer('longBreak')}
    >
      long break
    </button>
  </div>