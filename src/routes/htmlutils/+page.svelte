<script>
  import {
    Heading,
    P,
    Breadcrumb,
    BreadcrumbItem,
    Textarea,
    Button,
    Label,
    Input,
    ButtonGroup,
  } from "flowbite-svelte";
  import prettify from "@liquify/prettify";

  let inputText = "";
  let outputText = "";

  const prettifyHtml = async () => {
    try {
      outputText = await prettify.format(inputText, {
        language: "html",
        indentSize: 2,
      });
    } catch (error) {
      console.error(error);
      outputText = inputText;
    }
  };

  const minifyHtml = () => {
    outputText = inputText.replace(/\s+/g, " ").trim();
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>HTML Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input HTML</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input HTML"
          rows="5"
          placeholder="Input HTML"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <ButtonGroup>
        <Button on:click={prettifyHtml}>Prettify</Button>
        <Button on:click={minifyHtml}>Minify</Button>
      </ButtonGroup>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Output HTML</span>
        <Textarea
          bind:value={outputText}
          id="message"
          name="message"
          label="Output HTML"
          rows="4"
          placeholder="Output HTML"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
          disabled
        />
      </Label>
    </form>
  </div>
</div>
