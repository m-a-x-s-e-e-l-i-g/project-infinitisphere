<script lang="ts">
  import * as Sheet from "$lib/components/ui/sheet";
  import { Input } from "$lib/components/ui/input";
  import { Label } from "$lib/components/ui/label";
  import Icon from 'svelte-awesome';
  import gear from 'svelte-awesome/icons/gear';
  import { ticketId, credits } from '$lib/stores.js';
</script>

<Sheet.Root>
  <Sheet.Trigger style="position:absolute;left:10px;top:5px;">
    <Icon data={gear} label="Settings" style="fill:white"/>
  </Sheet.Trigger>
  <Sheet.Content side=left>
    <Sheet.Header>
      <Sheet.Title>Settings</Sheet.Title>
      <Sheet.Description>
      </Sheet.Description>
    </Sheet.Header>
    <div class="flex flex-col" style="margin-top:2em;">
      <Label class="flex-auto" for="ticketId">ticketId</Label>
      <Input type="number" class="flex-auto" id="ticketId" bind:value={$ticketId}/>
    </div>
    <div class="flex flex-col" style="margin-top:2em;">
      <Label class="flex-auto" for="credits">credits per ticket</Label>
      <Input type="number" class="flex-auto" id="credits" bind:value={$credits}/>
    </div>
    <Sheet.Footer class="absolute bottom-5 left-5 right-5"> 
      <Sheet.Close class="absolute right-0 bottom-2">
        <a href="https://www.maxmade.nl?utm_source=project-infinitisphere&utm_medium=referral" target="_blank" rel="noreferrer">
          <img src="img/logo-MAXmade-FFF.svg" alt="MAXmade" class="h-4 mx-auto"/>
        </a>
      </Sheet.Close>
    </Sheet.Footer>
  </Sheet.Content>
</Sheet.Root>