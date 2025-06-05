<script>
    let {
        heightREM = 1.25,
        backgroundColorRGBA = "rgba(50,50,50,255)",
        borderColorRGBA = "rgba(0,0,0,255)",
        children = undefined,
        class: clazz = "",
    } = $props();
</script>

<div
    style="
        height: {heightREM}rem;
        background-color: {backgroundColorRGBA};
        aspect-ratio: 1/cos(30deg);
        clip-path: polygon(50% -50%, 100% 50%, 50% 150%, 0 50%);
        display: flex;
        align-items: center;
        justify-content: center;
    "
    class={clazz}
>
    <span class="text-white text-[0.67rem] font-semibold">
        {@render children?.()}
    </span>
</div>