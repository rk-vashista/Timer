<script>
  export let showSettings;
  export let settings;
  export let updateSettings;

  let localSettings = { ...settings };

  function handleSave() {
    updateSettings(localSettings);
  }

  function handleClose() {
    showSettings = false;
  }
</script>

{#if showSettings}
  <div class="fixed inset-0 bg-black/30 backdrop-blur-sm flex items-center justify-center p-4 z-50">
    <div class="bg-white text-gray-800 p-8 rounded-2xl w-full max-w-md shadow-2xl">
      <h2 class="text-2xl font-bold mb-6 text-gray-700">Timer Settings</h2>
      <div class="space-y-6">
        {#each Object.entries(localSettings) as [mode, time]}
          <div>
            <label for={mode} class="block mb-2 text-sm font-medium text-gray-600 capitalize">
              {mode.replace(/([A-Z])/g, ' $1').trim()}
            </label>
            <div class="flex gap-2">
              <div class="flex-1">
                <label for={`${mode}-hours`} class="sr-only">Hours</label>
                <input
                  type="number"
                  id={`${mode}-hours`}
                  bind:value={time.hours}
                  min="0"
                  max="23"
                  class="w-full px-3 py-2 bg-gray-100 border border-gray-300 rounded-lg focus:ring-2 focus:ring-gray-400 focus:border-transparent"
                  placeholder="Hours"
                />
              </div>
              <div class="flex-1">
                <label for={`${mode}-minutes`} class="sr-only">Minutes</label>
                <input
                  type="number"
                  id={`${mode}-minutes`}
                  bind:value={time.minutes}
                  min="0"
                  max="59"
                  class="w-full px-3 py-2 bg-gray-100 border border-gray-300 rounded-lg focus:ring-2 focus:ring-gray-400 focus:border-transparent"
                  placeholder="Minutes"
                />
              </div>
            </div>
          </div>
        {/each}
      </div>
      <div class="mt-8 flex justify-end gap-4">
        <button
          on:click={handleClose}
          class="px-4 py-2 text-gray-600 hover:text-gray-800 transition-colors duration-300"
        >
          Cancel
        </button>
        <button
          on:click={handleSave}
          class="px-4 py-2 bg-gray-800 text-white rounded-lg hover:bg-gray-700 transition-colors duration-300"
        >
          Save Changes
        </button>
      </div>
    </div>
  </div>
{/if}

