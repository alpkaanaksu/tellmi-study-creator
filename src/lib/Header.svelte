<script>
    import { page, study } from "../stores"
</script>

<nav>
    <div class="top-menu">
        {#if $study.settings}
            <span class="menu">
                {#each ["settings", "items", "sets", "schedule", "images"] as p}
                    <span style={$page === p ? "font-weight: 700;" : ""} on:click={() => $page = p}>{p.charAt(0).toUpperCase() + p.slice(1)}</span> { " | " } 
                {/each}
                <span style={$page === "save" ? "font-weight: 700;" : ""} on:click={() => $page = "save"}>Save</span>
            </span>
        {/if}
    </div>

    <div class="nav-container">
        <div class="nav-title">
            <h2>Tellmi Study Creator</h2>
        </div>

        <div>
            <a href="/settings">⚙️</a>
            <a href="/instructions">instructions</a>
        </div>
    </div>
</nav>

<style>
    nav {
        position: fixed;
        top: 0;
        width: 100%;
    }
    .nav-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 16px;
        border-bottom: 1px solid lightgray;
        background-color: #ffffff;
    }

    .nav-title {
        display: flex;
    }

    .nav-container h2 {
        margin: 0;
    }

    .menu {
        margin: 0 auto;
        background-color: #efefef;
        border-radius: 99px;
        padding: 8px 16px;
        cursor: pointer;
    }

    .top-menu {
        position: fixed;
        top: 1rem;
        width: 100%;
        text-align: center;
        margin: 0 auto;
    }

    a {
        z-index: 500;
    }
</style>