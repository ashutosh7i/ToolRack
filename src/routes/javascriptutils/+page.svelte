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

  const prettifyJs = async () => {
    try {
      outputText = await prettify.format(inputText, {
        language: "javascript",
        indentSize: 2,
      });
    } catch (error) {
      console.error(error);
      outputText = inputText;
    }
  };

  const minifyJs = () => {
    outputText = inputText.replace(/\s+/g, " ").trim();
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>JavaScript Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input JavaScript</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input JavaScript"
          rows="5"
          placeholder="Input JavaScript"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <ButtonGroup>
        <Button on:click={prettifyJs}>Prettify</Button>
        <Button on:click={minifyJs}>Minify</Button>
      </ButtonGroup>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Output JavaScript</span>
        <Textarea
          bind:value={outputText}
          id="message"
          name="message"
          label="Output JavaScript"
          rows="4"
          placeholder="Output JavaScript"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
          disabled
        />
      </Label>
    </form>
  </div>
</div>
