<script>
    let {
        href,
        children = undefined,
    } = $props();
</script>

<a
    target="_blank"
    rel="noreferrer"
    class="cursor-pointer text-blue-600 underline-offset-2 hover:underline"
    href={href}
>
    {#if children}
    {@render children?.()}
    {:else}
    {href}
    {/if}
</a>