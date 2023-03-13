<script>
  let showModal = true;
  export let isPromo = false;               // This is a Prop. It'll be exported with a default boolean value.
  export let message = 'default message';   // This is a Prop. It'll be exported with a default message.
</script>                                   <!-- Props can be overriden (see 'App.svelte' example) -->

{#if showModal}
  <div class="backdrop" class:promo={isPromo}>
    <div class="modal">
      <p>{message}</p>             <!-- With Props, this variable now renders components reusable. -->
    </div>
  </div>
{/if}

<style>
  .backdrop{
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0,0,0,0.8);
  }
  .modal{
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;;
    text-align: center;
    background: white;
  }
  .promo .modal{
    background: crimson;
    color: white;
  }
</style>