<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  let sectionEl;
  let cards = [];

  const projects = [
    {
      num: '01',
      year: '2026',
      title: 'Lifeline',
      description:
        'Integrated healthcare platform for appointments, medicine purchases, real-time doctor chat, and QRIS payments.',
      tags: ['Next.js', 'Laravel', 'WebSocket']
    },
    {
      num: '02',
      year: '2026',
      title: 'Efwan Chapter',
      description:
        'Event ticketing platform with automated DOKU QRIS settlement, email delivery, and QR attendee verification.',
      tags: ['Fullstack', 'Payments', 'QR systems']
    },
    {
      num: '03',
      year: '2024',
      title: 'OCR Engine',
      description:
        'Cross-platform OCR application powered by Flutter and Laravel Filament, with asynchronous queue processing.',
      tags: ['Flutter', 'Laravel', 'Queues']
    },
    {
      num: '04',
      year: '2024',
      title: 'Smelting KIOSK',
      description:
        'Interactive Android self-service kiosk delivering operational announcements and visitor information.',
      tags: ['Android', 'Java', 'UI systems']
    },
    {
      num: '05',
      year: '2022—23',
      title: 'Suara Nahdliyin',
      description:
        'Fast-loading Astro news platform with automated scraping, real-time search, RBAC, and protections against XSS, CSRF, and SQL injection.',
      tags: ['Astro.js', 'Security', 'RBAC']
    },
    {
      num: '06',
      year: '2025',
      title: 'SPK Decision System',
      description:
        'Scientific decision-making application implementing MEREC and MARCOS algorithms for alternative ranking.',
      tags: ['Python', 'Tailwind', 'Modeling']
    }
  ];

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);

    const ctx = gsap.context(() => {
      gsap.from(cards, {
        scrollTrigger: {
          trigger: sectionEl,
          start: 'top 75%',
          toggleActions: 'play none none none'
        },
        y: 40,
        opacity: 0,
        stagger: 0.12,
        duration: 0.85,
        ease: 'power2.out'
      });
    }, sectionEl);

    return () => ctx.revert();
  });
</script>

<section id="work" bind:this={sectionEl} class="border-b hairline">
  <div class="flex flex-col justify-between gap-6 border-b hairline px-6 py-8 md:flex-row md:items-end md:px-8">
    <div>
      <p class="mono mb-5 text-xs">03 / SELECTED WORK</p>
      <h2 class="text-4xl font-medium tracking-tight md:text-7xl">Things I’ve built.</h2>
    </div>
    <p class="max-w-xs text-sm leading-relaxed opacity-60">
      A selection of production platforms, mobile tools, and digital systems created for real people and real constraints.
    </p>
  </div>

  <div class="grid md:grid-cols-2">
    {#each projects as project, i}
      <article
        bind:this={cards[i]}
        class="project-card border-b hairline px-6 py-8 {i % 2 === 0 ? 'md:border-r' : ''} md:px-8"
      >
        <div class="mb-20 flex justify-between">
          <span class="mono text-xs">{project.num}</span>
          <span class="mono text-xs opacity-50">{project.year}</span>
        </div>
        <h3 class="mb-3 text-2xl font-medium">{project.title}</h3>
        <p class="mb-6 max-w-md text-sm leading-relaxed opacity-60">{project.description}</p>
        <div class="flex flex-wrap gap-2 text-xs">
          {#each project.tags as tag}
            <span class="border hairline px-2 py-1">{tag}</span>
          {/each}
        </div>
      </article>
    {/each}
  </div>
</section>
