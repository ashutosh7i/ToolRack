<script>
  import Markdoc from "./Markdoc.svelte";
  import Callout from "./Callout.svelte";

  let doc = `# Hello, world!`;

  const config = {
    tags: {
      callout: {
        render: "Callout",
        description: "Display the enclosed content in a callout box",
        children: ["paragraph", "tag", "list"],
        attributes: {
          type: {
            type: String,
            default: "note",
            matches: ["check", "error", "note", "warning"],
          },
        },
      },
    },
  };

  const components = new Map([["Callout", Callout]]);
</script>

<div class="flex">
  <div class="w-1/2 p-4">
    <h2 class="text-lg font-bold mb-4">Edit Markdown</h2>
    <textarea bind:value={doc} class="w-full h-full"></textarea>
  </div>
  <div class="w-1/2 p-4">
    <h2 class="text-lg font-bold mb-4">Preview</h2>
    <Markdoc {doc} {config} {components} key={doc} />
  </div>
</div>
