<script lang="ts">
    import type { Gear } from "@/schemas/story";
    import GearElement from "./Misc/Gear.svelte";
    import Card from "./Card.svelte";

    export let rumors: string[] = [];
    export let gear: Gear[] = []
</script>

<Card icon="fa fa-comment" title="Rumors">
    <div class="content">
        <ul>
        {#each rumors as rumor}
            <li>{rumor}</li>
        {/each}
        </ul>
    </div>
</Card>

<Card icon="fa fa-cogs" title="Gear">
    {#each gear as g}
        <GearElement gear={g} />
    {/each}
</Card>
