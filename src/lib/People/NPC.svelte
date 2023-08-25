<script lang="ts">
    import type { Npc } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Card from "../Card.svelte";

    export let npc: Npc;
</script>

<Card
    icon="fa fa-user"
    title={npc.name}
>
    <div class="content">
        <p>
        {#each npc.tags as tag}
            <span class="tag">{tag}</span>&ensp;
        {/each}
        </p>
    {#if npc.description !== undefined}
        <SvelteMarkdown source={npc.description} />
    {/if}
    </div>
</Card>

