<script>
    let maxClick = $state(2);
    let cnt = $state(0); // tip: https://svelte.dev/docs/svelte/$state


    function onClick() {
      // tip: Since DOM (i.e., the webpage content) will automatically update based on values, [<p id="info">Remaining Number of Clicks: {cnt}</p>]
      // we only need to change the cnt number here.
      cnt += 1;
    }
  </script>

  <h1>Donald's VIS Site</h1>
  <img
    width="200px"
    src="https://media1.tenor.com/m/K43VoRlNvB8AAAAC/yamazaki-eat.gif"
  />
  <div>
    You can click up to
    <select
    /*tip: bind the select action to change the maxClick value. https://svelte.dev/docs/svelte/bind#select-bind:value */
        bind:value={maxClick}
        /*tip: define what will happen after click. Maybe you want to update the remaining number of clikc when click a new maxClick value */
        onchange={() => (cnt = 0)}>
      {#each [2, 4, 6] as optionNum}
        <option value={optionNum}>
          {optionNum}
        </option>
      {/each}
    </select>
    times
  </div>
  <button onclick={onClick}> Click Me </button>

  <!-- tip: use {#if...} template syntax here (https://svelte.dev/docs/svelte/if) so that the content below will automatically update when cnt value changes -->
    <!-- `the content below should only show when cnt >0` -->
  {#if cnt < maxClick}
    <p id="info">Remaining Number of Clicks: {cnt}</p>
  {:else}
    <!-- The content below should only shown when cnt =0 -->
    <p>No more clicks allowed</p>
  {/if}


  <style>
    body {
      font-family: Arial, Helvetica, sans-serif;
    }
    button {
      background-color: #44aa66;
      /* background-color: blue; */
      color: white;
      font-size: xx-large;
      padding: 10px 20px;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
  </style>
