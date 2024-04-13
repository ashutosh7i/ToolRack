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

  const compressCss = () => {
    outputText = inputText
      .replace(/\s+/g, " ")
      .replace(/;\s/g, ";")
      .replace(/:\s/g, ":")
      .replace(/,\s/g, ",")
      .replace(/\{\s/g, "{")
      .replace(/\}\s/g, "}")
      .replace(/\s\{/g, "{")
      .replace(/\s\}/g, "}")
      .replace(/\n/g, "");
  };

  const prettifyCss = async () => {
    try {
      outputText = await prettify.format(inputText, {
        language: "css",
        indentSize: 2,
      });
    } catch (error) {
      console.error(error);
      outputText = inputText;
    }
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>CSS Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <h3 class="text-xl font-medium text-gray-900 dark:text-gray-100">
        CSS Utilities
      </h3>
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input CSS</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input CSS"
          rows="5"
          placeholder="Input CSS"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <h4 class="text-md font-medium text-gray-900 dark:text-gray-100">
        Actions
      </h4>
      <ButtonGroup>
        <Button on:click={prettifyCss}>Prettify</Button>
        <Button on:click={compressCss}>Compress</Button>
      </ButtonGroup>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Output CSS</span>
        <Textarea
          bind:value={outputText}
          id="message"
          name="message"
          label="Output CSS"
          rows="4"
          placeholder="Output CSS"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
          disabled
        />
      </Label>
    </form>
  </div>
</div>
