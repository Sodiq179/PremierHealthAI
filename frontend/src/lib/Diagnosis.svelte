<script lang="ts">
  import { Tile, Content } from "carbon-components-svelte";
  import { onMount } from "svelte";
  import { PharmacistSocket } from "../types";
  import SvelteMarkdown from "svelte-markdown";

  let ddx = "";
  let qa = "";

  onMount(async () => {


    // cds_ddx
    PharmacistSocket.on("cds_ddx", (x) => {
      console.log(x);
      ddx = x.replaceAll("\n", "\n\n");
    });

    // cds_qa
    PharmacistSocket.on("cds_qa", (x) => {
      console.log(x);
      qa = x.replaceAll("\n", "\n\n");
    });
  });
</script>

<div class="flex gap-2 border-solid h-full">
  <div class="w-1/2 border-gray-600 border-2 border-solid h-full">
    <Tile>
      <p>Potential Diagnosis</p>
    </Tile>
    <div class="h-full m-2">
      <Content class="text-base prose text-lg" >
        <SvelteMarkdown source={ddx} />
      </Content>
    </div>
  </div>
  <div class="w-1/2 border-gray-600 border-2 border-solid h-full">
    <Tile>
      <p>Clarifications</p>
    </Tile>
    <div class="h-full m-2">
      <Content class="text-base prose text-lg">
        <SvelteMarkdown source={qa} />
      </Content>
    </div>
  </div>
</div>
