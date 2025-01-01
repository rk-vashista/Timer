<script>
  import { onMount } from 'svelte';
  import ModeButtons from './ModeButtons.svelte';
  import FlipClock from './FlipClock.svelte';
  import Controls from './Controls.svelte';
  import SettingsModal from './SettingsModal.svelte';

  let time = { hours: 0, minutes: 25, seconds: 0 };
  let isRunning = false;
  let timerInterval;
  let mode = 'pomodoro';
  let settings = {
    pomodoro: { hours: 0, minutes: 25 },
    shortBreak: { hours: 0, minutes: 5 },
    longBreak: { hours: 0, minutes: 15 }
  };
  let showSettings = false;

  function setTimer(newMode) {
    mode = newMode;
    stopTimer();
    time = { 
      hours: settings[mode].hours, 
      minutes: settings[mode].minutes, 
      seconds: 0 
    };
  }

  function startTimer() {
    if (!isRunning) {
      isRunning = true;
      let totalSeconds = (time.hours * 3600) + (time.minutes * 60) + time.seconds;
      
      timerInterval = setInterval(() => {
        if (totalSeconds > 0) {
          totalSeconds--;
          time = {
            hours: Math.floor(totalSeconds / 3600),
            minutes: Math.floor((totalSeconds % 3600) / 60),
            seconds: totalSeconds % 60
          };
        } else {
          stopTimer();
        }
      }, 1000);
    }
  }

  function stopTimer() {
    isRunning = false;
    clearInterval(timerInterval);
  }

  function resetTimer() {
    stopTimer();
    setTimer(mode);
  }

  function updateSettings(newSettings) {
    settings = newSettings;
    setTimer(mode);
    showSettings = false;
  }

  onMount(() => {
    setTimer('pomodoro');
  });
</script>

<div class="w-full max-w-xl flex flex-col items-center gap-8">
  <ModeButtons {mode} {setTimer} />
  <FlipClock {time} />
  <Controls {isRunning} {startTimer} {stopTimer} {resetTimer} bind:showSettings />
  <SettingsModal bind:showSettings {settings} {updateSettings} />
</div>

