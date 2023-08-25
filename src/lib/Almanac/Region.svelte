<script lang="ts">
    import type {
        Region,
        Area,
        Steading,
        Site,
        Encounter,
        Treasure,
        Monster,
    } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import AreaElement from "./Area.svelte";
    import SteadingElement from "./Steading.svelte";
    import SiteElement from "./Site.svelte";
    import EncounterElement from "./Encounter.svelte";
    import MonsterElement from "./Monster.svelte";
    import TreasureElement from "./Treasure.svelte";
    import Card from "../Card.svelte";

    export let region: Region;

    let areas: Area[] = [];
    let steadings: Steading[] = [];
    let sites: Site[] = [];
    let encounters: Encounter[] = [];
    let treasures: Treasure[] = [];
    let monsters: Monster[] = [];
    if (region.children !== undefined) {
        areas = region.children.filter((c) => c.type === "area") as Area[];
        steadings = region.children.filter(
            (c) => c.type === "steading",
        ) as Steading[];
        sites = region.children.filter((c) => c.type === "site") as Site[];
        encounters = region.children.filter(
            (c) => c.type === "encounter",
        ) as Encounter[];
        treasures = region.children.filter(
            (c) => c.type === "treasure",
        ) as Treasure[];
        monsters = region.children.filter(
            (c) => c.type === "monster",
        ) as Monster[];
    }
</script>

<Card
    icon="fa fa-globe"
    title={`Region &middot; ${region.name}`}
>
    <div class="content">
        <p>
        {#each region.tags as tag}
            <span class="tag">{tag}</span>&ensp;
        {/each}
        </p>
    {#if region.description !== undefined}
        <SvelteMarkdown source={region.description} />
    {/if}
    {#if region.moves !== undefined}
        <h4>Moves</h4>
        <Moves moves={region.moves} />
    {/if}
    </div>
{#if areas.length > 0}
    {#each areas as area}
        <AreaElement area={area} />
    {/each}
{/if}
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
