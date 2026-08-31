<script lang="ts">
    import type { Snippet } from "svelte";
    import type { HTMLAttributes } from "svelte/elements";

    let {
        children,
        class: className,
        ...attributes
    }: HTMLAttributes<HTMLDivElement> & { children?: Snippet } = $props();
</script>

<div
    {...attributes}
    class={[
        "flex w-full max-w-sm flex-col gap-4 rounded-lg bg-clip-padding bg-white p-6 shadow-md shadow-yellow-300",
        className,
    ]}
>
    {@render children?.()}
</div>
