<!-- 
     Event forwarding example: let's export showModal to our App.svelte component.
     This allows us to use a reference here, pointing to a variable inside the ancestor component (App.svelte).
-->

<script>
  export let showModal = false;        // the showModel variable will be exported (and can also be overriden)
  export let isPromo = false;
  export let message = 'default message';
</script>

{#if showModal}
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <div class="backdrop" class:promo={isPromo} on:click>     <!-- "on:click" is seen as an event forwarded  -->   
    <div class="modal">                                     <!-- we want it to affect the "backdrop" div -->  
      <p>{message}</p>                                      <!-- but it could be put in any div you want -->
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