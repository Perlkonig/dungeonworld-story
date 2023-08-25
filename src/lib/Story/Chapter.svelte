<script lang="ts">
    import type { Chapter } from "@/schemas/story";
    import SvelteMarkdown from "svelte-markdown";
    import Card from "../Card.svelte";

    export let chapter: Chapter;
    export let index: number;
</script>

<Card
    icon="fa fa-book"
    title={`Chapter ${index}${chapter.name !== undefined ? `&nbsp;&middot;&nbsp;${chapter.name}` : ""}`}
>
    <div class="content">
        <SvelteMarkdown source={chapter.text} />
    </div>
</Card>
