<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';

  let isOpen = false;
  let menuPanel;
  let menuButton;

  function toggleMenu() {
    isOpen = !isOpen;
    if (isOpen) {
      gsap.fromTo(
        menuPanel,
        { opacity: 0, y: -10, scale: 0.96 },
        { opacity: 1, y: 0, scale: 1, duration: 0.25, ease: 'power2.out' }
      );
    }
  }

  function closeMenu() {
    if (isOpen) {
      gsap.to(menuPanel, {
        opacity: 0,
        y: -8,
        scale: 0.96,
        duration: 0.18,
        ease: 'power2.in',
        onComplete: () => {
          isOpen = false;
        }
      });
    }
  }

  onMount(() => {
    function handleClickOutside(event) {
      if (
        isOpen &&
        menuPanel &&
        !menuPanel.contains(event.target) &&
        menuButton &&
        !menuButton.contains(event.target)
      ) {
        closeMenu();
      }
    }

    window.addEventListener('click', handleClickOutside);
    return () => window.removeEventListener('click', handleClickOutside);
  });
</script>

<header class="relative z-20 flex items-center justify-between border-b hairline px-6 py-5 md:px-8">
  <div class="mono text-xs uppercase tracking-widest md:text-sm">Malang, Indonesia</div>
  <div class="mono hidden text-xs md:block">11 · 11 · 2026</div>
  <div class="mono hidden text-xs md:block">Available for work</div>

  <button
    bind:this={menuButton}
    on:click={toggleMenu}
    type="button"
    aria-expanded={isOpen}
    aria-controls="menu-panel"
    class="group flex items-center gap-3 text-xs uppercase tracking-widest cursor-pointer select-none"
  >
    <span>Menu</span>
    <span class="block w-7 space-y-1">
      <i class="block h-px bg-black transition-transform duration-200 {isOpen ? 'translate-y-1 rotate-45' : ''}"></i>
      <i class="ml-2 block h-px bg-black transition-transform duration-200 {isOpen ? '-translate-y-1 -rotate-45 !ml-0' : ''}"></i>
    </span>
  </button>

  {#if isOpen}
    <div
      bind:this={menuPanel}
      id="menu-panel"
      class="menu-surface absolute right-6 top-16 z-30 w-56 border hairline p-5 shadow-lg md:right-8"
    >
      <nav class="flex flex-col gap-4 text-sm">
        <a href="#about" on:click={closeMenu} class="hover:underline">About</a>
        <a href="#work" on:click={closeMenu} class="hover:underline">Selected work</a>
        <a href="#experience" on:click={closeMenu} class="hover:underline">Experience</a>
        <a href="#toolkit" on:click={closeMenu} class="hover:underline">Toolkit</a>
        <a href="#contact" on:click={closeMenu} class="hover:underline">Contact</a>
      </nav>
    </div>
  {/if}
</header>
