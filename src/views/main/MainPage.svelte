<script lang="ts">
    import Card from '../card/Card.svelte';
    import TopBar from './TopBar.svelte';

    async function fetchInven() {
        const url = 'https://ikkanezumi-meow-fairy.koyeb.app/maple-inven';
        const response = await fetch(url);
        return await response.json();
    }
</script>

<div class="nav">
    <TopBar />
</div>
<div class="content">
    {#await fetchInven() then articles}
        {#each articles as article}
            <Card image={article.icon ?? './favicon.png'} title={article.title} link={article.link}
            ></Card>
        {/each}
    {/await}
    <Card image="./favicon.png"></Card>
</div>

<style lang="scss">
    $nav-height: 50px;
    .nav {
        display: flex;
        align-items: center;
        border: solid 1px #5d6582;
        border-radius: 5px;
        margin: 5px;
        padding: 5px;
        width: calc(100% - 20px);
        height: $nav-height - 20px;
        background: #ffffff;
    }

    .content {
        border: solid 1px #5d6582;
        border-radius: 5px;
        margin: 5px;
        padding: 5px;
        width: calc(100% - 20px);
        height: calc(100% - $nav-height - 20px);
        background: #ffffff;
    }
</style>
