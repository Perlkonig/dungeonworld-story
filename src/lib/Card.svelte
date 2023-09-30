<script lang="ts">
    export let icon: string;
    export let title: string;
    export let expanded = true;
</script>

<div class="card">
    <header class="card-header" on:click="{() => (expanded = !expanded)}">
        <p class="card-header-title">
            <span class="icon"><i class="{icon}" aria-hidden="true"></i></span
            >&nbsp;{@html title}
        </p>
        <button class="card-header-icon" aria-label="more options">
            <span class="icon">
                {#if expanded}
                    <i class="fa fa-angle-down" aria-hidden="true"></i>
                {:else}
                    <i class="fa fa-angle-left" aria-hidden="true"></i>
                {/if}
            </span>
        </button>
    </header>
    {#if expanded}
        <div class="card-content">
            <slot />
        </div>
    {/if}
</div>
