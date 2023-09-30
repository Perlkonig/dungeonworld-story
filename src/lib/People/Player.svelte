<script lang="ts">
    import type { Player } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Card from "../Card.svelte";

    export let player: Player;
    let showModal = false;
</script>

<Card
    icon="fa fa-user"
    title="{`${player.name}, level ${player.level} ${player.class} (${player.player})`}"
    expanded="{false}"
>
    <div class="media">
        {#if "id" in player && player.id !== undefined && player.id.length > 0}
            <figure class="media-left" on:click="{() => (showModal = true)}">
                <p class="image is-square">
                    <img src="images/{player.id}.jpeg" />
                </p>
            </figure>
            <div class="modal{showModal ? ' is-active' : ''}">
                <div
                    class="modal-background"
                    on:click="{() => (showModal = false)}"
                ></div>
                <div class="modal-content">
                    <p class="image is-square">
                        <img src="images/{player.id}.jpeg" alt="" />
                    </p>
                </div>
                <button
                    class="modal-close is-large"
                    aria-label="close"
                    on:click="{() => (showModal = false)}"
                ></button>
            </div>
        {/if}
        <div class="media-content">
            <div class="content">
                <SvelteMarkdown source="{player.story}" />
            </div>
        </div>
    </div>
</Card>

<style>
    .media-left {
        width: 10%;
    }
</style>
