<script lang="ts">
    import * as imported from "@/assets/story.json";
    import type { DungeonWorldStory } from "./schemas/story";
    import TimeAgo from "javascript-time-ago";
    import en from "javascript-time-ago/locale/en";
    import Almanac from "./lib/Almanac.svelte";
    import Story from "./lib/Story.svelte";
    import People from "./lib/People.svelte";
    import Misc from "./lib/Misc.svelte";
    TimeAgo.addDefaultLocale(en);

    // @ts-ignore
    const updated = new Date(__BUILD_DATE__);
    const timeAgo = new TimeAgo("en-CA");
    const strTimeAgo = timeAgo.format(updated);
    const story: DungeonWorldStory = imported as DungeonWorldStory;
    let activeTab: "people" | "almanac" | "story" | "misc" = "story";
</script>

<main class="container p-6">
    <div class="level">
        <div class="level-left">
            <div class="level-item">
                <div>
                    <p class="title">Dungeon World: The Story So Far</p>
                </div>
            </div>
        </div>
    </div>
    <h1 class="title">{story.name}</h1>
    <h2 class="subtitle">
        Last updated <span title="{updated.toString()}">{strTimeAgo}</span>
    </h2>

    <div class="tabs">
        <ul>
            <li class="{activeTab === 'story' ? 'is-active' : ''}">
                <a on:click="{() => (activeTab = 'story')}">The Story</a>
            </li>
            <li class="{activeTab === 'people' ? 'is-active' : ''}">
                <a on:click="{() => (activeTab = 'people')}">The People</a>
            </li>
            <li class="{activeTab === 'almanac' ? 'is-active' : ''}">
                <a on:click="{() => (activeTab = 'almanac')}">The World</a>
            </li>
            <li class="{activeTab === 'misc' ? 'is-active' : ''}">
                <a on:click="{() => (activeTab = 'misc')}">Miscellanea</a>
            </li>
        </ul>
    </div>

    {#if activeTab === "almanac"}
        <Almanac almanac="{story.almanac}" />
    {:else if activeTab === "story"}
        <Story story="{story.story}" />
    {:else if activeTab === "people"}
        <People people="{story.people}" />
    {:else if activeTab === "misc"}
        <Misc rumors={story.misc?.rumors} gear={story.misc?.gear} />
    {/if}
</main>

<style>
    /* .logo {
        height: 8em;
        padding: 1.5em;
    }
    #contentContainer {
        width: 100%;
        height: 110vh;
    } */
</style>
