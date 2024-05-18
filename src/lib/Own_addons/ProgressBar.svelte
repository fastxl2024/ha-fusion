<script>
  export let value = 0;
  export let name = '';

  // Function to determine color based on value
  function getColor() {
    if (value < 65) {
      return 'green';
    } else if (value >= 65 && value <= 85) {
      return 'orange';
    } else {
      return 'red';
    }
  }
</script>

<style>
  .bar {
    width: 100%;
    height: 20px;
    background-color: lightgray;
    position: relative;
    border-radius: 4px;
    margin-bottom: 8px;
  }

  .fill {
    height: 100%;
    border-radius: 4px;
  }

  .label {
    position: absolute;
    top: -24px;
    left: 0;
    width: 100%;
    text-align: center;
    font-size: 14px;
    font-weight: bold;
    color: aqua;
  }
</style>

<div class="label">{name} - {value}%</div>
<div class="bar">
  <div class="fill" style="width: {value}%; background-color: {getColor()}"></div>
</div>