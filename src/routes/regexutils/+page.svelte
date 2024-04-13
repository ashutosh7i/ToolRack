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
    Table,
    TableBody,
    TableBodyCell,
    TableBodyRow,
    TableHead,
    TableHeadCell,
  } from "flowbite-svelte";

  let regexInput = "";
  let testString = "";
  let matchResult = "";

  const testRegex = () => {
    try {
      const regex = new RegExp(regexInput);
      matchResult = regex.test(testString) ? "Match found" : "No match found";
    } catch (error) {
      console.error(error);
    }
  };
</script>

<h1>under developemnt</h1>
<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>Regex Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input Regex</span>
        <Textarea
          bind:value={regexInput}
          id="regex"
          name="regex"
          label="Input Regex"
          rows="2"
          placeholder="Input Regex"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Test String</span>
        <Textarea
          bind:value={testString}
          id="testString"
          name="testString"
          label="Test String"
          rows="2"
          placeholder="Test String"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <ButtonGroup>
        <Button on:click={testRegex}>Test Regex</Button>
      </ButtonGroup>

      <Table>
        <TableHead>
          <TableHeadCell>Result</TableHeadCell>
        </TableHead>
        <TableBody class="divide-y">
          <TableBodyRow>
            <TableBodyCell>{matchResult}</TableBodyCell>
          </TableBodyRow>
        </TableBody>
      </Table>
    </form>
  </div>
</div>
