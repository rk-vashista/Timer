<script>
    export let time;
  
    function formatNumber(num) {
      return num.toString().padStart(2, '0');
    }
  </script>
  
  <div class="text-8xl font-mono bg-gray-800 rounded-lg p-8 shadow-lg">
    {formatNumber(time.hours)}:{formatNumber(time.minutes)}:{formatNumber(time.seconds)}
  </div>