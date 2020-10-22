<script>
  import { Button, Label, Spacer, TextArea } from "@budibase/bbui"
  import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
  
  let score
  let suggestions
  let triedSubmit = false
  let scores = [1,2,3,4,5,6,7,8,9,10]

  const setScore = newScore => () => score = newScore
  const isScore = testScore => score === testScore

  const submit = () => {
    triedSubmit = true

    if (!score) return

    dispatch("submitted", {
      type: "NPS",
      npsScore: score,
      suggestions
    })
  }
</script>

<div class="container">

  <Label large black>
    How likely are you to recommend Budibase to a <br/> friend or colleague?
  </Label>

  <div class="score-container">
    {#each scores as thisScore}
      <div class:primary={score === thisScore} class:secondary={score !== thisScore}>
        <Button 
          primary={score === thisScore} 
          secondary={score !== thisScore} 
          on:click={() => score = thisScore}>{thisScore}</Button>
      </div>
    {/each}
  </div>

  {#if triedSubmit && !score}
    <span class="error-label">Please choose a score</span>
  {/if}

  <Spacer large/>

  <Label large black>
    What could we do to improve?
  </Label>
  
  <TextArea 
    placeholder="add privacy settings" 
    bind:value={suggestions}/>

  <Spacer large/>

  <div class="button-container">
    <Button primary on:click={submit}>Submit</Button>
  </div>


</div>

<style>

  .score-container {
    display: flex;
    gap: var(--spacing-s);
  }

  .container {
    text-align: start;
    max-width: 500px;
    min-width: 500px;
    max-height: 266px;
    min-height: 266px;
  }



  .button-container {
    text-align: right;
  }

  /* overriding button behaviour - sizing issues*/
  .primary > :global(button) {
    border-width: 1px;
  }
  
  .primary > :global(button:hover) {
    background-color: var(--ink) !important;
    color: var(--white) !important;
  }

  .error-label {
    color: var(--red);
    font-size: var(--font-size-m);
    font-family: var(--font-sans);
  }

</style>