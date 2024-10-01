<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import "./styles.css";

  let currentDateAndTime: Date;
  let dateStr: string;
  let timeStr: string;

  function updateTime() {
    currentDateAndTime = new Date();
    dateStr = currentDateAndTime.toLocaleDateString(undefined, { weekday: 'short', month: 'short', day: 'numeric' });
    timeStr = currentDateAndTime.toLocaleTimeString();
  }

  let interval: number;

  onMount(() => {
    updateTime(); // Initial update
    interval = setInterval(updateTime, 1000);
  });

  onDestroy(() => {
    clearInterval(interval);
  });
</script>

<div class="clock-application">
  <div class="nav-bar">
    <ul>
      <li><a href="/">Alarm</a></li>
      <li><a href="/">Clock</a></li>
      <li><a href="/">Timer</a></li>
      <li><a href="/">Stopwatch</a></li>
    </ul>
  </div>
  <div class="clock-face">
    <center>
      <h1>
        {timeStr}
      </h1>
      {dateStr}
    </center>
  </div>
</div>

<style>
  ul {
    display: flex;
    justify-content: center;
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  li {
    margin-right: 50px;
  }
  h1 {
    font-size: 4em;
  }
  .clock-application {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: white;
  }
</style>
