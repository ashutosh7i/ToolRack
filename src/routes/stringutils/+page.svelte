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
  let charCount = 0;
  let wordCount = 0;
  let lineCount = 0;

  const updateCounts = () => {
    charCount = inputText.length;
    wordCount = inputText.split(/\s+/).filter(Boolean).length;
    lineCount = inputText.split(/\n/).length;
  };

  const toLowerCase = () => {
    outputText = inputText.toLowerCase();
  };

  const toUpperCase = () => {
    outputText = inputText.toUpperCase();
  };

  const reverseString = () => {
    outputText = inputText.split("").reverse().join("");
  };

  const trimString = () => {
    outputText = inputText.trim();
  };

  const removeSymbols = () => {
    outputText = inputText.replace(/[^\w\s]|_/g, "");
  };

  const removeNumbers = () => {
    outputText = inputText.replace(/[0-9]/g, "");
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>String Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6" on:input={updateCounts}>
      <h3 class="text-xl font-medium text-gray-900 dark:text-gray-100">
        String Utilities
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

      <div class="flex items-start">
        <div>
          <span class="text-gray-900 dark:text-gray-100">Character Count</span>
          <Input
            id="char-count"
            class="mb-6 bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
            disabled
            bind:value={charCount}
          />
        </div>
        <div>
          <span class="text-gray-900 dark:text-gray-100">Word Count</span>
          <Input
            id="word-count"
            class="mb-6 bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
            disabled
            bind:value={wordCount}
          />
        </div>
        <div>
          <span class="text-gray-900 dark:text-gray-100">Line Count</span>
          <Input
            id="line-count"
            class="mb-6 bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
            disabled
            bind:value={lineCount}
          />
        </div>
      </div>

      <h4 class="text-md font-medium text-gray-900 dark:text-gray-100">
        Actions
      </h4>
      <ButtonGroup>
        <Button on:click={toLowerCase}>lowercase</Button>
        <Button on:click={toUpperCase}>UPPERCASE</Button>
        <Button on:click={reverseString}>Reverse</Button>
        <Button on:click={trimString}>Trim</Button>
        <Button on:click={removeSymbols}>Remove Symbols</Button>
        <Button on:click={removeNumbers}>Remove Numbers</Button>
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
