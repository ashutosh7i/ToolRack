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
  import { xmlToJsonUtil } from "xml-to-json-util";

  let inputText = "";
  let outputText = "";

  const prettifyXml = async () => {
    try {
      outputText = await prettify.format(inputText, {
        language: "xml",
        indentSize: 2,
      });
    } catch (error) {
      console.error(error);
      outputText = inputText;
    }
  };

  const convertToJson = () => {
    outputText = JSON.stringify(xmlToJsonUtil(inputText), null, 2);
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>XML Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input XML</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input XML"
          rows="5"
          placeholder="Input XML"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <ButtonGroup>
        <Button on:click={prettifyXml}>Prettify</Button>
        <Button on:click={convertToJson}>Convert to JSON</Button>
      </ButtonGroup>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Output</span>
        <Textarea
          bind:value={outputText}
          id="message"
          name="message"
          label="Output"
          rows="4"
          placeholder="Output"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
          disabled
        />
      </Label>
    </form>
  </div>
</div>
