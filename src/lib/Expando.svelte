<script>

    import Icon from "@iconify/svelte";

    let {
        label = '',
        children = undefined,
        expanded = $bindable(true),
        downloado = false,
    } = $props();

    let height = $state(0)

</script>


<div
    class="
        border-t border-t-gray-200
        overflow-hidden transition-[height]
    "
    class:h-10={downloado || !expanded}
    style="height:{!downloado && expanded ? `calc(2.5rem + ${height}px)` : ''}"
>
    {#if downloado}
        <a
            href=https://doi.org/10.57931/2550666
            class="
                block font-bold text-base text-gray-800 hover:text-blue-600
                px-4 py-2 cursor-pointer uppercase w-full text-start
            "
            target="_blank"
            rel="noreferrer"
        >
            <Icon
                class="inline-block"
                inline
                icon="ph:arrow-square-out-bold"
            /> Get the Data
        </a>
    {:else}
        <button
            class="
                font-bold text-base text-gray-800 hover:text-blue-600
                px-4 py-2 cursor-pointer uppercase w-full text-start
            "
            onclick={() => { expanded = !expanded }}
        >
            <Icon
                class="inline-block"
                inline
                icon={expanded ? "ph:caret-down-bold" : "ph:caret-right-bold"}
            /> {label}
        </button>
        <div
            class="px-4 py-2" 
            bind:clientHeight={height}
        >
            {@render children?.()}
        </div>
    {/if}
</div>
