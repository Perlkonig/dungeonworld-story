<script lang="ts">
    import type { Chapter } from "@/schemas/story";
    import ChapterElement from "./Story/Chapter.svelte";

    export let story: Chapter[] = [];
    const reversed = [...story].reverse();
</script>

{#each reversed as chapter, i}
    <ChapterElement chapter="{chapter}" index="{reversed.length - i}" />
{/each}
