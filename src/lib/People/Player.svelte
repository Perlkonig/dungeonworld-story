<script lang="ts">
    import type { Player } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Card from "../Card.svelte";

    export let player: Player;
</script>

<Card
    icon="fa fa-user"
    title={`${player.name}, level ${player.level} ${player.class} (${player.player})`}
    expanded={false}
>
    <div class="content">
        <SvelteMarkdown source={player.story} />
    </div>
</Card>
