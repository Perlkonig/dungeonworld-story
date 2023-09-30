<script lang="ts">
    import type { Monster } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Moves from "./Moves.svelte";
    import Card from "../Card.svelte";

    export let monster: Monster;
</script>

<Card
    icon="fa fa-exclamation-triangle"
    title="{`Monster &middot; ${monster.name}`}"
>
    <div class="content">
        <p>
            {#each monster.tags as tag}
                <span class="tag">{tag}</span>&ensp;
            {/each}
        </p>
        {#if monster.hp !== undefined || monster.damage !== undefined || monster.armor !== undefined}
            <p>
                {#if monster.damage !== undefined}
                    <b>Damage:</b> {monster.damage}<br />
                {/if}
                {#if monster.hp !== undefined}
                    <b>HP:</b> {monster.hp}<br />
                {/if}
                {#if monster.armor !== undefined}
                    <b>Armor:</b> {monster.armor}
                {/if}
            </p>
        {/if}
        {#if monster.description !== undefined}
            <SvelteMarkdown source="{monster.description}" />
        {/if}
        {#if monster.moves !== undefined}
            <h4>Moves</h4>
            <Moves moves="{monster.moves}" />
        {/if}
        {#if monster.instincts !== undefined}
            <h4>Instincts</h4>
            <ul>
                {#each monster.instincts as instinct}
                    <li>{instinct}</li>
                {/each}
            </ul>
        {/if}
    </div>
</Card>
