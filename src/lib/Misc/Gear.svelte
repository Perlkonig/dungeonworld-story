<script lang="ts">
    import type { Gear } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Card from "../Card.svelte";

    export let gear: Gear;
    let showModal = false;
</script>

<Card icon="fa fa-user" title="{gear.name}">
    <div class="media">
        {#if "id" in gear && gear.id !== undefined && gear.id.length > 0}
            <figure class="media-left" on:click="{() => (showModal = true)}">
                <p class="image is-square">
                    <img src="images/{gear.id}.jpeg" />
                </p>
            </figure>
            <div class="modal{showModal ? ' is-active' : ''}">
                <div
                    class="modal-background"
                    on:click="{() => (showModal = false)}"
                ></div>
                <div class="modal-content">
                    <p class="image is-square">
                        <img src="images/{gear.id}.jpeg" alt="" />
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
                    {#each gear.tags as tag}
                        <span class="tag">{tag}</span>&ensp;
                    {/each}
                </p>
                {#if gear.description !== undefined}
                    <SvelteMarkdown source="{gear.description}" />
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
