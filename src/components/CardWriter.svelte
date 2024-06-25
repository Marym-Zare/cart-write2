<script>
  import Card from "./Card.svelte";
  import { keyToCardMap } from "$lib/keyCode.js";
  let cards = [];

  function handleKeyPress(event) {
    const key = event.key;
    const newCard = {
      id: Math.random().toString(32).slice(2, 8),
      title: keyToCardMap[key],
    };
    if (newCard.title) {
      if (cards.length >= 20) {
        cards = [newCard, ...cards.slice(1)];
      } else {
        cards = [newCard, ...cards];
      }
    }
  }
</script>

<div class="flex items-center gap-4 justify-start flex-wrap">
  {#each cards as card (card.id)}
    <Card card={card.title} />
  {/each}
</div>
<svelte:window on:keydown|preventDefault={handleKeyPress} />
