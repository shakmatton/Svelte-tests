<!-- 
     Event forwarding example: let's export showModal to our App.svelte component.
     This allows us to use a reference here, pointing to a variable inside the ancestor component (App.svelte).

     Event modifier: useful when we want to easiyl change how we react to certain events (like submit events).
     You must use it with a pipe. For example, click:on|self={...}
     
     Here are some examples of event modifiers:

     once - makes sure the event can fire only once (removes handler)
     preventDefault - prevents the default action (run e.preventDefault())
     self - only fires the event if the component element is the target
-->

<script>
  export let showModal = false;        // the showModel variable will be exported (and can also be overriden)
  export let isPromo = false;
  export let message = 'default message';
</script>

{#if showModal}  <!-- svelte-ignore a11y-click-events-have-key-events -->

  <!-- "on:click" is seen as an event forwarded. -->
  <!-- We want it to affect the "backdrop" div, but it could be put in any div you want. -->

  <div class="backdrop" class:promo={isPromo} on:click|self>   <!-- the 'self' affects ONLY this backdrop div -->     
    <div class="modal">                                        <!-- it won't affect any other div whatsover -->
      <p>{message}</p>                                      
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