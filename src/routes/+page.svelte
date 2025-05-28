<script lang="ts">
  import SDK from '@sizecredit/sdk';

  const sdk = new SDK({
    markets: [],
    version: 'v1.7',
  });

  let errorInput = '';
  let calldataInput = '';
  let decodedError = '';
  let decodedCalldata = '';

  $: if (errorInput) {
    try {
      decodedError = sdk.decode.error(errorInput);
    } catch (e: unknown) {
      decodedError = `Error decoding: ${e instanceof Error ? e.message : String(e)}`;
    }
  } else {
    decodedError = '';
  }

  $: if (calldataInput) {
    try {
      decodedCalldata = sdk.decode.calldata(calldataInput);
    } catch (e: unknown) {
      decodedCalldata = `Error decoding: ${e instanceof Error ? e.message : String(e)}`;
    }
  } else {
    decodedCalldata = '';
  }
</script>

<h1>Size SDK</h1>

<div class="decoder-section">
  <h2>Decode Error</h2>
  <div class="input-group">
    <input 
      type="text" 
      bind:value={errorInput} 
      placeholder="Enter error data to decode"
    />
  </div>
  {#if decodedError}
    <pre class="result">{decodedError}</pre>
  {/if}
</div>

<div class="decoder-section">
  <h2>Decode Calldata</h2>
  <div class="input-group">
    <input 
      type="text" 
      bind:value={calldataInput} 
      placeholder="Enter calldata to decode"
    />
  </div>
  {#if decodedCalldata}
    <pre class="result">{decodedCalldata}</pre>
  {/if}
</div>

<style>
  .decoder-section {
    margin: 2rem 0;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 8px;
  }

  .input-group {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  input {
    flex: 1;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  button {
    padding: 0.5rem 1rem;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  button:hover {
    background-color: #45a049;
  }

  .result {
    background-color: #f5f5f5;
    padding: 1rem;
    border-radius: 4px;
    overflow-x: auto;
  }
</style>
