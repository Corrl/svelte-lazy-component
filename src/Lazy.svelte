<script>
    export let init

    let Comp

    init().then(res => {
        Comp = res.default
    })

</script>

{#if Comp}
    <slot {Comp}></slot>
{/if}

