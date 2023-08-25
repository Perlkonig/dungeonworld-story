<script lang="ts">
    import type {
        Area,
        Steading,
        Site,
        Encounter,
        Treasure,
        Monster,
    } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import SteadingElement from "./Steading.svelte";
    import SiteElement from "./Site.svelte";
    import EncounterElement from "./Encounter.svelte";
    import MonsterElement from "./Monster.svelte";
    import TreasureElement from "./Treasure.svelte";
    import Card from "../Card.svelte";

    export let area: Area;

    let steadings: Steading[] = [];
    let sites: Site[] = [];
    let encounters: Encounter[] = [];
    let treasures: Treasure[] = [];
    let monsters: Monster[] = [];
    if (area.children !== undefined) {
        steadings = area.children.filter(
            (c) => c.type === "steading",
        ) as Steading[];
        sites = area.children.filter((c) => c.type === "site") as Site[];
        encounters = area.children.filter(
            (c) => c.type === "encounter",
        ) as Encounter[];
        treasures = area.children.filter(
            (c) => c.type === "treasure",
        ) as Treasure[];
        monsters = area.children.filter(
            (c) => c.type === "monster",
        ) as Monster[];
    }
</script>

<Card
    icon="fa fa-map"
    title={`Area &middot; ${area.name}`}
>
    <div class="content">
        <p>
        {#each area.tags as tag}
            <span class="tag">{tag}</span>&ensp;
        {/each}
        </p>
    {#if area.description !== undefined}
        <SvelteMarkdown source={area.description} />
    {/if}
    {#if area.moves !== undefined}
        <h4>Moves</h4>
        <Moves moves={area.moves} />
    {/if}
    </div>
{#if steadings.length > 0}
    {#each steadings as steading}
        <SteadingElement steading={steading} />
    {/each}
{/if}
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
{#if treasures.length > 0}
    {#each treasures as treasure}
        <TreasureElement treasure={treasure} />
    {/each}
{/if}
{#if monsters.length > 0}
    {#each monsters as monster}
        <MonsterElement monster={monster} />
    {/each}
{/if}
</Card>

