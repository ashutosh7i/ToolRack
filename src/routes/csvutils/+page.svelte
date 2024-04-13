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
  import Papa from "papaparse";

  let inputText = "";
  let outputText = "";

  const removeTrailingSpaces = (text) => text.replace(/\s+$/, "");

  const formatCsv = () => {
    const cleanedInput = removeTrailingSpaces(inputText);
    const parsed = Papa.parse(cleanedInput, { header: true });
    const trimmedData = parsed.data.map((row) => {
      const trimmedRow = {};
      for (const key in row) {
        trimmedRow[key.trim()] = row[key].trim();
      }
      return trimmedRow;
    });
    outputText = Papa.unparse(trimmedData);
  };

  const validateCsv = () => {
    const cleanedInput = removeTrailingSpaces(inputText);
    const parsed = Papa.parse(cleanedInput, { header: true });
    outputText = parsed.errors.length
      ? JSON.stringify(parsed.errors, null, 2)
      : "No errors found";
  };

  const convertToJSON = () => {
    const cleanedInput = removeTrailingSpaces(inputText);
    const parsed = Papa.parse(cleanedInput, { header: true });
    if (parsed.errors.length) {
      alert("Cannot convert to JSON due to errors in the CSV data.");
    } else {
      outputText = JSON.stringify(parsed.data, null, 2);
    }
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>CSV Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <h3 class="text-xl font-medium text-gray-900 dark:text-gray-100">
        CSV Utilities
      </h3>
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input CSV</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input CSV"
          rows="5"
          placeholder="Input CSV"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <h4 class="text-md font-medium text-gray-900 dark:text-gray-100">
        Actions
      </h4>
      <ButtonGroup>
        <Button on:click={formatCsv}>Format</Button>
        <Button on:click={validateCsv}>Validate</Button>
        <Button on:click={convertToJSON}>Convert to JSON</Button>
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
