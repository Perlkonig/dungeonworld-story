<script lang="ts">
    import type { Npc } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Card from "../Card.svelte";

    export let npc: Npc;
    let showModal = false;
</script>

<Card icon="fa fa-user" title="{npc.name}">
    <div class="media">
        {#if "id" in npc && npc.id !== undefined && npc.id.length > 0}
            <figure class="media-left" on:click="{() => (showModal = true)}">
                <p class="image is-3by4">
                    <img src="images/{npc.id}.png" />
                </p>
            </figure>
            <div class="modal{showModal ? ' is-active' : ''}">
                <div
                    class="modal-background"
                    on:click="{() => (showModal = false)}"
                ></div>
                <div class="modal-content">
                    <p class="image is-3by4">
                        <img src="images/{npc.id}.png" alt="" />
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
                <p>
                    {#each npc.tags as tag}
                        <span class="tag">{tag}</span>&ensp;
                    {/each}
                </p>
                {#if npc.description !== undefined}
                    <SvelteMarkdown source="{npc.description}" />
                {/if}
            </div>
        </div>
    </div></Card
>

<style>
    .media-left {
        width: 10%;
    }
</style>
