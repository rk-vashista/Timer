<script>
  export let showSettings;
  export let settings;
  export let updateSettings;

  let localSettings = { ...settings };

  function handleSave() {
    updateSettings(localSettings);
  }
</script>

{#if showSettings}
  <div class="fixed inset-0 bg-black/80 flex items-center justify-center p-4">
    <div class="bg-gray-800 p-8 rounded-lg w-full max-w-md">
      <h2 class="text-2xl font-bold mb-6">Timer Settings</h2>
      <div class="space-y-4">
        {#each ['pomodoro', 'shortBreak', 'longBreak'] as mode}
          <div>
            <label for={mode} class="block mb-1 capitalize">{mode.replace(/([A-Z])/g, ' $1').trim()}</label>
            <div class="flex gap-2">
              <input
                type="number"
                id={`${mode}-hours`}
                bind:value={localSettings[mode].hours}
                min="0"
                max="23"
                class="w-full bg-gray-700 text-white px-3 py-2 rounded"
                placeholder="Hours"
              />
              <input
                type="number"
                id={`${mode}-minutes`}
                bind:value={localSettings[mode].minutes}
                min="0"
                max="59"
                class="w-full bg-gray-700 text-white px-3 py-2 rounded"
                placeholder="Minutes"
              />
            </div>
          </div>
        {/each}
      </div>
      <div class="mt-6 flex justify-end">
        <button
          on:click={handleSave}
          class="px-4 py-2 bg-white text-black rounded"
        >
          Save
        </button>
      </div>
    </div>
  </div>
{/if}

