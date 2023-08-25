<script lang="ts">
    import type { Almanac } from "@/schemas/story";
    import Card from "./Card.svelte";
    import Region from "./Almanac/Region.svelte";

    export let almanac: Almanac = [];
    let showModal = false;
</script>

<Card
    title="World Map"
    icon="fa fa-map"
    expanded={false}
>
    <figure class="image is-5by4" on:click="{() => showModal = true}">
        <img src="/map.png">
    </figure>
    <div class="modal{showModal ? " is-active" : ""}">
        <div class="modal-background"></div>
        <div class="modal-content">
          <p class="image is-5by4">
            <img src="/map.png" alt="">
          </p>
        </div>
        <button class="modal-close is-large" aria-label="close" on:click="{() => showModal = false}"></button>
    </div>
</Card>

{#each almanac as region}
    <Region region={region} />
{/each}

