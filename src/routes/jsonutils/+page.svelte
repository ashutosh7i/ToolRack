<script>
  import { Toast } from "flowbite-svelte";
  import { CheckCircleSolid, CloseCircleSolid } from "flowbite-svelte-icons";
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
  let isValidJson = false;
  let showSuccessToast = false;
  let showErrorToast = false;

  const validateJson = () => {
    try {
      JSON.parse(inputText);
      isValidJson = true;
      showSuccessToast = true;
      showErrorToast = false;
    } catch (e) {
      isValidJson = false;
      showErrorToast = true;
      showSuccessToast = false;
    }
  };

  const formatJson = () => {
    try {
      const parsed = JSON.parse(inputText);
      outputText = JSON.stringify(parsed, null, 2);
      isValidJson = true;
    } catch (e) {
      isValidJson = false;
    }
  };

  const sortKeys = () => {
    try {
      const parsed = JSON.parse(inputText);
      const sorted = sortObject(parsed);
      outputText = JSON.stringify(sorted, null, 2);
      isValidJson = true;
    } catch (e) {
      isValidJson = false;
    }
  };

  function sortObject(obj) {
    if (Array.isArray(obj)) {
      return obj.map(sortObject);
    } else if (typeof obj === "object" && obj !== null) {
      return Object.keys(obj)
        .sort()
        .reduce((res, key) => {
          res[key] = sortObject(obj[key]);
          return res;
        }, {});
    } else {
      return obj;
    }
  }
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>JSON Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6" on:input={validateJson}>
      {#if showSuccessToast}
        <Toast dismissable={false} color="green">
          <svelte:fragment slot="icon">
            <CheckCircleSolid class="w-5 h-5" />
            <span class="sr-only">Check icon</span>
          </svelte:fragment>
          Valid JSON.
        </Toast>
      {/if}

      {#if showErrorToast}
        <Toast dismissable={false} color="red">
          <svelte:fragment slot="icon">
            <CloseCircleSolid class="w-5 h-5" />
            <span class="sr-only">Error icon</span>
          </svelte:fragment>
          Invalid JSON.
        </Toast>
      {/if}
      <h3 class="text-xl font-medium text-gray-900 dark:text-gray-100">
        JSON Utilities
      </h3>
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input JSON</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input JSON"
          rows="5"
          placeholder="Input JSON"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <h4 class="text-md font-medium text-gray-900 dark:text-gray-100">
        Actions
      </h4>
      <ButtonGroup>
        <Button on:click={formatJson}>Format</Button>
        <Button on:click={sortKeys}>Sort Keys</Button>
      </ButtonGroup>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Output JSON</span>
        <Textarea
          bind:value={outputText}
          id="message"
          name="message"
          label="Output JSON"
          rows="4"
          placeholder="Output JSON"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
          disabled
        />
      </Label>
    </form>
  </div>
</div>
