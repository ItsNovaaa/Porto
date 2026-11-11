<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';

  let heroContainer;
  let titleLines = [];
  let ovalOne;
  let ovalTwo;
  let introCard;

  onMount(() => {
    const ctx = gsap.context(() => {
      // Animate headline lines reveal
      gsap.from(titleLines, {
        y: 60,
        opacity: 0,
        stagger: 0.15,
        duration: 1.1,
        ease: 'power3.out'
      });

      // Animate intro text & badge
      gsap.from(introCard, {
        y: 30,
        opacity: 0,
        duration: 1,
        delay: 0.35,
        ease: 'power2.out'
      });

      // Smooth floating animation for decorative ovals
      gsap.to(ovalOne, {
        y: -14,
        x: 8,
        rotation: 4,
        duration: 4,
        repeat: -1,
        yoyo: true,
        ease: 'sine.inOut'
      });

      gsap.to(ovalTwo, {
        y: 12,
        x: -6,
        rotation: -3,
        duration: 4.8,
        repeat: -1,
        yoyo: true,
        ease: 'sine.inOut'
      });
    }, heroContainer);

    return () => ctx.revert();
  });
</script>

<div bind:this={heroContainer} class="hero-height relative grid grid-cols-1 md:grid-cols-5">
  <div class="relative col-span-3 flex flex-col justify-between border-r hairline px-6 py-14 md:px-8 md:py-20">
    <div class="display-title uppercase select-none">
      <span bind:this={titleLines[0]}>Building</span>
      <span bind:this={titleLines[1]}>Digital</span>
      <span bind:this={titleLines[2]}>Experiences</span>
    </div>

    <div class="mt-14 flex items-end justify-between gap-8 text-xs uppercase tracking-wide md:mt-0">
      <p class="max-w-[15rem] leading-relaxed">
        Fullstack & mobile developer building useful digital products with clarity and care.
      </p>
      <span class="mono">01 — 06</span>
    </div>

    <!-- Decorative Oval 1 -->
    <div
      bind:this={ovalOne}
      class="oval pointer-events-none absolute left-[20%] top-[27%] h-20 w-36 md:h-28 md:w-52"
    ></div>
  </div>

  <div class="relative col-span-2 flex flex-col justify-between px-6 py-14 md:px-8 md:py-20">
    <div bind:this={introCard} class="max-w-xs md:ml-auto">
      <p class="mono mb-8 text-xs">01 / INTRODUCTION</p>
      <h2 class="mb-4 text-2xl font-medium leading-tight md:text-3xl">
        I turn complex ideas into simple, dependable experiences.
      </h2>
      <p class="text-sm leading-relaxed opacity-60">
        Information Technology student at Politeknik Negeri Malang, with hands-on experience across web, mobile, APIs, and technical leadership.
      </p>
    </div>

    <a
      href="mailto:faforite36@gmail.com"
      class="oval mx-auto flex h-32 w-32 items-center justify-center text-center text-sm transition hover:bg-black hover:text-white md:h-40 md:w-40"
    >
      Start a<br />conversation
    </a>

    <!-- Decorative Oval 2 -->
    <div
      bind:this={ovalTwo}
      class="oval pointer-events-none absolute bottom-[22%] right-[22%] h-16 w-28 opacity-60 md:h-24 md:w-40"
    ></div>
  </div>
</div>
