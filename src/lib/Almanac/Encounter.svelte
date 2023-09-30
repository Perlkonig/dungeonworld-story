<script lang="ts">
    import type { Encounter } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import Card from "../Card.svelte";

    export let encounter: Encounter;
</script>

<Card icon="fa fa-users" title="{`Encounter &middot; ${encounter.name}`}">
    <div class="content">
        <p>
            {#each encounter.tags as tag}
                <span class="tag">{tag}</span>&ensp;
            {/each}
        </p>
        {#if encounter.description !== undefined}
            <SvelteMarkdown source="{encounter.description}" />
        {/if}
        {#if encounter.moves !== undefined}
            <h4>Moves</h4>
            <Moves moves="{encounter.moves}" />
        {/if}
    </div>
</Card>
