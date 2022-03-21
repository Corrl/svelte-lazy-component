<script>
    import Lazy from './Lazy.svelte'

    let showLazyComp
    let text = "passed text"
</script>

<div>
    <button on:click={() => showLazyComp = true}>
        show Lazy loading Component
    </button>
</div>

<p>text in parent: {text}</p>

{#if showLazyComp}
    <Lazy init={() => import('./SomeComponent.svelte')} let:Comp>
        <Comp bind:text on:click={() => console.log('btn clicked in lazy loaded component')}/>
    </Lazy>
{/if}

