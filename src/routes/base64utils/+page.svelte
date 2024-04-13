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

  let inputText = "";
  let outputText = "";

  const encodeBase64 = () => {
    outputText = btoa(inputText);
  };

  const decodeBase64 = () => {
    outputText = atob(inputText);
  };

  const toText = () => {
    outputText = decodeURIComponent(escape(window.atob(inputText)));
  };

  const toBinary = () => {
    outputText = Array.prototype.map
      .call(atob(inputText), function (c) {
        return "0" + c.charCodeAt(0).toString(2);
      })
      .join(" ");
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>Base64 Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <h3 class="text-xl font-medium text-gray-900 dark:text-gray-100">
        Base64 Utilities
      </h3>
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input String</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input Text"
          rows="5"
          placeholder="Input String"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <h4 class="text-md font-medium text-gray-900 dark:text-gray-100">
        Actions
      </h4>
      <ButtonGroup>
        <Button on:click={encodeBase64}>Encode</Button>
        <Button on:click={decodeBase64}>Decode</Button>
        <Button on:click={toText}>To Text</Button>
        <Button on:click={toBinary}>To Binary</Button>
      </ButtonGroup>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Output String</span>
        <Textarea
          bind:value={outputText}
          id="message"
          name="message"
          label="Output Text"
          rows="4"
          placeholder="Output String"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
          disabled
        />
      </Label>
    </form>
  </div>
</div>
