<script lang="ts">
    import type { Player, Npc } from "@/schemas/story";
    import PlayerElement from "./People/Player.svelte";
    import NpcElement from "./People/NPC.svelte";
    import Card from "./Card.svelte";

    export let people: (Player | Npc)[] = [];
    const players = people
        .filter((p) => "player" in p)
        .sort((a, b) => a.name.localeCompare(b.name)) as Player[];
    const npcs = people
        .filter((p) => !("player" in p))
        .sort((a, b) => a.name.localeCompare(b.name)) as Npc[];
</script>

<Card icon="fa fa-users" title="Players">
    {#each players as player}
        <PlayerElement player="{player}" />
    {/each}
</Card>

<Card icon="fa fa-users" title="NPCs">
    {#each npcs as npc}
        <NpcElement npc="{npc}" />
    {/each}
</Card>
