<script>
    let isLoading = false;
  
    export async function handleClick() {
      // Set isLoading to true to show the spinner while loading
      isLoading = true;
  
      try {
        // Perform your asynchronous operation (e.g., API call, data fetching)
        await fetchSomeData();
      } catch (error) {
        console.error('Error:', error);
      } finally {
        // Set isLoading back to false after the operation is complete
        isLoading = false;
      }
    }
  
    export async function fetchSomeData() {
      // Simulating an asynchronous operation
      return new Promise((resolve) => {
        setTimeout(resolve, 2000); // Simulating a 2-second delay
      });
    }
  </script>
  
  <button on:click = {handleClick} disabled = {isLoading} class="btn btn-square">
    {#if isLoading}
    <span class="spinner"></span> Loading...
  {:else}
    Click me
  {/if}
    <span class="loading loading-spinner"></span>
  </button>
  
