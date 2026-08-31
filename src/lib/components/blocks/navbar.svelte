<script lang="ts">
    import { onMount } from "svelte";

    import {getAuthToken, getMe, logOut, type CurrentUser} from "$lib/auth.svelte";

    let me = $state<CurrentUser | null>(null);

    onMount(async () => {
        if (!getAuthToken()) return;

        try {
            me = await getMe();
        } catch {
            // The layout handles invalid tokens; keep the navbar usable if the API is unavailable.
        }
    });
</script>

<div class="w-full flex flex-row flex-1 min-w-0 h-auto mb-2 bg-white p-5 shadow-md justify-between">
    <div class="flex flex-row items-start justify-start gap-5 align-middle">
        <a href="/" class="font-bold text-xl">Outreach DB</a>
        <a class="self-center text-md" href="/map">Map</a>
        {#if me?.permission_level === 0}
            <a class="self-center text-md" href="/admin">Admin</a>
        {/if}
    </div>
    <div class="flex flex-row items-start justify-start gap-5">
        {#if getAuthToken()}
            {#if me}
                <p>Hi, {me.first_name}</p>
            {/if}
            <a href="##" onclick={() => logOut()}>Logout</a>
        {:else}
            <a href="/login" class="nav-link">Login</a>
        {/if}
    </div>
</div>
<style>
    .nav-link {
        border-bottom: 2px solid transparent;
        transition: border-bottom 0.3s ease;
    }

    .nav-link:hover {
        border-bottom: 2px solid black;
    }
</style>
