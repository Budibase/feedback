  <script>
    export let primary, secondary
  </script>
  
  <button
    class:primary
    class:secondary
    on:click|preventDefault>
    <slot />
  </button>

<style>
  button {
    font-family: var(--font-sans);
    cursor: pointer;
    font-weight: 600;
    box-sizing: border-box;
    overflow: hidden;
    border-radius: var(--border-radius-s);
    color: var(--white);
    padding: var(--spacing-s) var(--spacing-l);
    transition: all 0.2s ease 0s;
    display: inline-flex;
    text-rendering: optimizeLegibility;
    text-decoration: none;
    min-width: auto;
    outline: none;
    font-feature-settings: "case" 1, "rlig" 1, "calt" 0;
    -webkit-box-align: center;
    user-select: none;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    margin: 0;
  }

  .primary {
    border: var(--border-black);
    background-color: var(--ink);
  }
  button.primary:hover:not([disabled]) {
    background-color: var(--white);
    color: var(--ink);
  }
  .secondary {
    border: var(--border-grey);
    background-color: white;
    color: var(--grey-8);
    font-weight: 500;
  }
  button.secondary:hover:not([disabled]) {
    background-color: var(--grey-2);
    color: var(--ink);
  }
  button:disabled {
    background-color: var(--grey-4);
    cursor: not-allowed;
    border: solid 1.5px var(--grey-4);
    color: var(--grey-5);
  }
</style>
