<script>
  import { DarkMode } from 'flowbite-svelte';
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger, Button, Input } from 'flowbite-svelte';
	import logo from '$lib/images/logo.png';
</script>
  
  <Navbar>
    <NavBrand href="/">
      <img src={logo} class="me-3 h-6 sm:h-9" alt="ToolRack Logo" />
      <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">ToolRack</span>
    </NavBrand>
    <div class="flex md:order-2">
      <DarkMode class="text-primary-500 dark:text-primary-600 border dark:border-gray-800" />
      <Button href="/stringutils" size="sm">Get started</Button>
      <NavHamburger />
    </div>
    <NavUl class="order-1">
      <NavLi href="/" active={true}>Home</NavLi>
      <NavLi href="/about">About</NavLi>
      <NavLi href="https://github.com/ashutosh7i/toolrack">Source</NavLi>
      <NavLi href="https://linkedin.com/in/ashutosh7i">Contact</NavLi>
    </NavUl>
    
  </Navbar>