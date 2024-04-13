<script>
  import {
    Heading,
    P,
    Breadcrumb,
    BreadcrumbItem,
    List,
    Li,
  } from "flowbite-svelte";
</script>

<Breadcrumb aria-label="Default breadcrumb example" solid>
  <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
  <BreadcrumbItem>About</BreadcrumbItem>
</Breadcrumb>

<div
  class="w-full h-full flex flex-col items-center justify-center bg-gray-100 dark:bg-gray-900"
>
  <div class="w-full h-full bg-white dark:bg-gray-800 p-6 rounded shadow">
    <Heading tag="h2" class="text-gray-900 dark:text-gray-100"
      >About Toolrack</Heading
    >
    <P class="text-gray-900 dark:text-gray-100">
      Welcome to ToolRack, your one-stop destination for a collection of online
      text manipulation utilities and more. Developed with a focus on simplicity
      and efficiency, ToolRack provides a wide range of tools to help you with
      various text-related tasks quickly and easily.
    </P>
    <Heading tag="h3" class="text-gray-900 dark:text-gray-100">Features</Heading
    >
    <List>
      <Li>String Tools</Li>
      <Li>JSON Viewer</Li>
      <Li>Markdown Editor</Li>
      <Li>QR Code Generator</Li>
      <Li>Regex Tester</Li>
      <Li>URL Encoder/Decoder</Li>
      <Li>XML Parser</Li>
      <Li>And More</Li>
    </List>
    <Heading tag="h3" class="text-gray-900 dark:text-gray-100"
      >Tech Stack</Heading
    >
    <P class="text-gray-900 dark:text-gray-100">
      ToolRack is built using the following technologies: Frontend: Svelte.js
      for the user interface, providing a fast and reactive experience. Backend:
      Node.js for server-side logic, handling requests and responses. QR Code
      Generation: qrcode.js library for generating QR codes dynamically.
      Markdown Rendering: Marked library for rendering Markdown content into
      HTML. Styling: Tailwind CSS for efficient and responsive styling.
    </P>
    <Heading tag="h3" class="text-gray-900 dark:text-gray-100"
      >Contributing</Heading
    >
    <P class="text-gray-900 dark:text-gray-100">
      ToolRack is an open-source project, and contributions are welcome! If you
      have ideas for new features, improvements, or bug fixes, feel free to
      contribute to the project on GitHub.
    </P>
    <Heading tag="h3" class="text-gray-900 dark:text-gray-100"
      >Contact me</Heading
    >
    <P class="text-gray-900 dark:text-gray-100">
      If you have any questions, feedback, or suggestions, don't hesitate to
      reach out to me. You can contact me via email at work@ashutosh7i.dev or
      through my GitHub repository.
    </P>
    <P class="text-gray-900 dark:text-gray-100">
      Thank you for using ToolRack!
    </P>
  </div>
</div>
