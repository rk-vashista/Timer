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
    <div class="fixed inset-0 bg-black/80 flex items-center justify-center">
      <div class="bg-gray-800 p-8 rounded-lg w-full max-w-md">
        <h2 class="text-2xl font-bold mb-6">Timer Settings</h2>
        <div class="space-y-4">
          <div>
            <label for="pomodoro" class="block mb-1">Pomodoro (minutes)</label>
            <input
              type="number"
              id="pomodoro"
              bind:value={localSettings.pomodoro}
              min="1"
              max="60"
              class="w-full bg-gray-700 text-white px-3 py-2 rounded"
            />
          </div>
          <div>
            <label for="shortBreak" class="block mb-1">Short Break (minutes)</label>
            <input
              type="number"
              id="shortBreak"
              bind:value={localSettings.shortBreak}
              min="1"
              max="30"
              class="w-full bg-gray-700 text-white px-3 py-2 rounded"
            />
          </div>
          <div>
            <label for="longBreak" class="block mb-1">Long Break (minutes)</label>
            <input
              type="number"
              id="longBreak"
              bind:value={localSettings.longBreak}
              min="1"
              max="60"
              class="w-full bg-gray-700 text-white px-3 py-2 rounded"
            />
          </div>
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