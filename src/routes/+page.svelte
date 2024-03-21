<script lang="ts">
    import { DateTime } from 'luxon';
    import { tick } from 'svelte';
    import QR from 'svelte-qr';
    import sha1 from 'crypto-js/sha1';
    import { ticketId, credits } from '$lib/stores.js';
    import { Button } from "$lib/components/ui/button";
    import GithubCorner from "$lib/components/ui/github-corner";
    import SettingsMenu from "$lib/components/ui/settings-menu";

    const vendorId = 28;
    let expiration = getNextExpiration();
    const unknown = 743;
    const empty = '';
    let hash = '';

    let renderQR = false;
    let qrString = '';

    $: {
        renderQR = false;
        hash = sha1(String($ticketId)).toString();
        qrString = `${vendorId}|${$ticketId}|${expiration}|${unknown}|${empty}|${$credits}|${hash}`;
        tick().then(() => {
            renderQR = true;
        });
    }

    let expirationHuman = DateTime.fromSeconds(expiration).toFormat('dd/MM/yyyy');

    function getNextExpiration() {
        const now = DateTime.now().setZone('Europe/Amsterdam');
        let nextExpiration = now.plus({ months: 4 }).startOf('month');

        return Math.floor(nextExpiration.toSeconds());
    }
</script>
<SettingsMenu />
<GithubCorner />
<div class="flex flex-col justify-center">
    <div style="width:60vw; height:60vw; margin:2rem auto;">
        <div class="bg-white p-1" style="width:100%; height:100%;">
            {#if renderQR}
                <QR text="{qrString}" />
            {/if}
        </div>
    </div>
    <div class="text-center" style="width:60vw;margin:0 auto;">
        <Button on:click={() => { $ticketId++; }}>New Ticket</Button>
    </div>
    <div style="width:60vw;margin:2rem auto;">
        <div class="flex justify-between">
            <p class="text-2xl mr-10">Ticket ID:</p>
            <p class="text-2xl">{$ticketId}</p>
        </div>
        <div class="flex justify-between">
            <p class="text-2xl mr-10">Expiration:</p>
            <p class="text-2xl">{expirationHuman}</p>
        </div>
        <div class="flex justify-between">
            <p class="text-2xl mr-10">Credits:</p>
            <p class="text-2xl">{$credits}</p>
        </div>
    </div>
</div>