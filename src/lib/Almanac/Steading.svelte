<script lang="ts">
    import type { Steading, Site, Encounter } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import SiteElement from "./Site.svelte";
    import EncounterElement from "./Encounter.svelte";
    import Card from "../Card.svelte";

    export let steading: Steading;

    let sites: Site[] = [];
    let encounters: Encounter[] = [];
    if (steading.children !== undefined) {
        sites = steading.children.filter((c) => c.type === "site") as Site[];
        encounters = steading.children.filter(
            (c) => c.type === "encounter",
        ) as Encounter[];
    }

</script>

<Card
    icon="fa fa-home"
    title={`Steading &middot; ${steading.name}`}
>
    <div class="content">
        <p>
        {#each steading.tags as tag}
            <span class="tag">{tag}</span>&ensp;
        {/each}
        </p>
    {#if steading.description !== undefined}
        <SvelteMarkdown source={steading.description} />
    {/if}
    {#if steading.moves !== undefined}
        <h4>Moves</h4>
        <Moves moves={steading.moves} />
    {/if}
    </div>
{#if sites.length > 0}
    {#each sites as site}
        <SiteElement site={site} />
    {/each}
{/if}
{#if encounters.length > 0}
    {#each encounters as encounter}
        <EncounterElement encounter={encounter} />
    {/each}
{/if}
</Card>
