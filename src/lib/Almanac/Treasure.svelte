<script lang="ts">
    import type { Treasure } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import Card from "../Card.svelte";

    export let treasure: Treasure;
</script>

<Card
    icon="fa fa-diamond"
    title={`Treasure &middot; ${treasure.name}`}
>
    <div class="content">
        <p>
        {#each treasure.tags as tag}
            <span class="tag">{tag}</span>&ensp;
        {/each}
        </p>
    {#if ( (treasure.weight !== undefined) || (treasure.value !== undefined) )}
        <p>
        {#if (treasure.weight !== undefined)}
            <b>Weight:</b> {treasure.weight}<br>
        {/if}
        {#if treasure.value !== undefined}
            <b>Value:</b> {treasure.value} coins
        {/if}
        </p>
    {/if}
    {#if treasure.description !== undefined}
        <SvelteMarkdown source={treasure.description} />
    {/if}
    {#if treasure.moves !== undefined}
        <h4>Moves</h4>
        <Moves moves={treasure.moves} />
    {/if}
    </div>
</Card>
