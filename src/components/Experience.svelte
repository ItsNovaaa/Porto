<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  let sectionEl;
  let items = [];

  const experiences = [
    {
      company: 'Efwan Chapter Indonesia',
      role: 'Freelance Fullstack Developer',
      year: '2026',
      description: 'Built automated ticketing with QRIS payments, attendee QR check-ins, and ticket mailers.'
    },
    {
      company: 'Fakta Data Yaqut',
      role: 'Freelance Fullstack Developer',
      year: '2026',
      description: 'Built a high-traffic public figure portal with Laravel, Next.js, and multi-role article management.'
    },
    {
      company: 'Rembang Migas & Sebaneh',
      role: 'Frontend & Mobile Developer',
      year: '2025',
      description: 'Engineered a responsive enterprise profile and an all-in-one Flutter mobile application.'
    },
    {
      company: 'PT. Smelting Gresik',
      role: 'Freelance Mobile Developer',
      year: '2024',
      description: 'Delivered an interactive self-service KIOSK for company operational information.'
    },
    {
      company: 'Dosen Ngoding',
      role: 'Freelance Fullstack Developer',
      year: '2024',
      description: 'Architected an OCR engine for Android and web with Laravel Filament and queue jobs.'
    },
    {
      company: 'PT. Sekawan Media',
      role: 'Intern Fullstack Developer',
      year: '2022—23',
      description: 'Contributed to corporate audit systems, software documentation, and client feature sprints.'
    }
  ];

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);

    const ctx = gsap.context(() => {
      gsap.from(items, {
        scrollTrigger: {
          trigger: sectionEl,
          start: 'top 75%',
          toggleActions: 'play none none none'
        },
        y: 25,
        opacity: 0,
        stagger: 0.1,
        duration: 0.75,
        ease: 'power2.out'
      });
    }, sectionEl);

    return () => ctx.revert();
  });
</script>

<section id="experience" bind:this={sectionEl} class="border-b hairline">
  <div class="border-b hairline px-6 py-8 md:px-8">
    <p class="mono mb-5 text-xs">05 / EXPERIENCE</p>
    <h2 class="text-4xl font-medium tracking-tight md:text-7xl">Where I’ve contributed.</h2>
  </div>

  <div class="grid md:grid-cols-2">
    {#each experiences as exp, i}
      <article
        bind:this={items[i]}
        class="border-b hairline px-6 py-7 {i % 2 === 0 ? 'md:border-r' : ''} md:px-8"
      >
        <div class="flex justify-between gap-4">
          <div class="min-w-0">
            <h3 class="break-words font-semibold">{exp.company}</h3>
            <p class="text-sm opacity-60">{exp.role}</p>
          </div>
          <span class="mono shrink-0 text-xs">{exp.year}</span>
        </div>
        <p class="mt-4 text-sm leading-relaxed opacity-60">{exp.description}</p>
      </article>
    {/each}
  </div>
</section>
