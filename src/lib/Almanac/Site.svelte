<script lang="ts">
    import type { Site, Encounter, Treasure, Monster } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import EncounterElement from "./Encounter.svelte";
    import MonsterElement from "./Monster.svelte";
    import TreasureElement from "./Treasure.svelte";
    import Card from "../Card.svelte";

    export let site: Site;

    let encounters: Encounter[] = [];
    let treasures: Treasure[] = [];
    let monsters: Monster[] = [];
    if (site.children !== undefined) {
        encounters = site.children.filter(
            (c) => c.type === "encounter",
        ) as Encounter[];
        treasures = site.children.filter(
            (c) => c.type === "treasure",
        ) as Treasure[];
        monsters = site.children.filter(
            (c) => c.type === "monster",
        ) as Monster[];
    }
</script>

<Card icon="fa fa-map-marker" title="{`Site &middot; ${site.name}`}">
    <div class="content">
        <p>
            {#each site.tags as tag}
                <span class="tag">{tag}</span>&ensp;
            {/each}
        </p>
        {#if site.description !== undefined}
            <SvelteMarkdown source="{site.description}" />
        {/if}
        {#if site.moves !== undefined}
            <h4>Moves</h4>
            <Moves moves="{site.moves}" />
        {/if}
    </div>
    {#if encounters.length > 0}
        {#each encounters as encounter}
            <EncounterElement encounter="{encounter}" />
        {/each}
    {/if}
    {#if treasures.length > 0}
        {#each treasures as treasure}
            <TreasureElement treasure="{treasure}" />
        {/each}
    {/if}
    {#if monsters.length > 0}
        {#each monsters as monster}
            <MonsterElement monster="{monster}" />
        {/each}
    {/if}
</Card>
