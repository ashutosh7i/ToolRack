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

  let inputText = "";
  let urlComponents = {};

  const parseUrl = () => {
    try {
      const url = new URL(inputText);
      urlComponents = {
        slashes: url.protocol.includes("https"),
        protocol: url.protocol,
        hash: url.hash,
        query: url.search,
        pathname: url.pathname,
        host: url.host,
        port: url.port,
        hostname: url.hostname,
        origin: url.origin,
        href: url.href,
      };
    } catch (error) {
      console.error(error);
    }
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>URL Utilities</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Input URL</span>
        <Textarea
          bind:value={inputText}
          id="message"
          name="message"
          label="Input URL"
          rows="5"
          placeholder="Input URL"
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <ButtonGroup>
        <Button on:click={parseUrl}>Parse URL</Button>
      </ButtonGroup>

      <Table>
        <TableHead>
          <TableHeadCell>Component</TableHeadCell>
          <TableHeadCell>Value</TableHeadCell>
        </TableHead>
        <TableBody class="divide-y">
          {#each Object.entries(urlComponents) as [key, value]}
            <TableBodyRow>
              <TableBodyCell>{key}</TableBodyCell>
              <TableBodyCell>{value}</TableBodyCell>
            </TableBodyRow>
          {/each}
        </TableBody>
      </Table>
    </form>
  </div>
</div>
