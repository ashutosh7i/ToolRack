<script>
  import QRCode from "qrcode";
  import {
    Button,
    Dropdown,
    DropdownItem,
    Label,
    Input,
    Breadcrumb,
    BreadcrumbItem,
  } from "flowbite-svelte";

  let text = "";
  let qrImage = "";
  let dataType = "Text";

  const generateQR = async () => {
    let dataToEncode;
    switch (dataType) {
      case "Phone Number":
        dataToEncode = `tel:${text}`;
        break;
      case "URL":
        dataToEncode = text.startsWith("http") ? text : `http://${text}`;
        break;
      case "Email Address":
        dataToEncode = `mailto:${text}`;
        break;
      default:
        dataToEncode = text;
    }

    try {
      qrImage = await QRCode.toDataURL(dataToEncode);
    } catch (err) {
      console.error(err);
    }
  };

  const downloadQR = () => {
    const link = document.createElement("a");
    link.href = qrImage;
    link.download = "QRCode.png";
    link.click();
  };
</script>

<div
  class="w-full h-full flex flex-col items-left justify-center bg-gray-100 dark:bg-gray-900"
>
  <Breadcrumb aria-label="Default breadcrumb example" solid>
    <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
    <BreadcrumbItem>QR Code Generator</BreadcrumbItem>
  </Breadcrumb>

  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <form class="flex flex-col space-y-6">
      <h3 class="text-xl font-medium text-gray-900 dark:text-gray-100">
        QR Code Generator
      </h3>
      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Text to encode:</span>
        <Input
          bind:value={text}
          class="bg-white dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        />
      </Label>

      <Label class="space-y-2">
        <span class="text-gray-900 dark:text-gray-100">Data Type:</span>
        <Button>
          {dataType}
          ⬇️
        </Button>
        <Dropdown>
          <DropdownItem on:click={() => (dataType = "Text")}>Text</DropdownItem>
          <DropdownItem on:click={() => (dataType = "Phone Number")}
            >Phone Number</DropdownItem
          >
          <DropdownItem on:click={() => (dataType = "URL")}>URL</DropdownItem>
          <DropdownItem on:click={() => (dataType = "Email Address")}
            >Email Address</DropdownItem
          >
        </Dropdown>
      </Label>

      <Button on:click={generateQR} size="sm" class=" self-center w-30 h-30"
        >Generate QR Code</Button
      >

      {#if qrImage}
        <div class="self-center">
          <h2
            class=" self-center text-md font-medium text-gray-900 dark:text-gray-100"
          >
            Your QR Code:
          </h2>
          <img class="self-center" src={qrImage} alt="Generated QR Code" />
          <Button on:click={downloadQR}>Download QR Code</Button>
        </div>
      {/if}
    </form>
  </div>
</div>
