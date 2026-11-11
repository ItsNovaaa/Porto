<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  let sectionEl;
  let cols = [];

  const toolkits = [
    {
      title: 'Backend & APIs',
      items: ['Laravel & PHP', 'Next.js & Node.js', 'Python & Go', 'RESTful APIs', 'WebSockets', 'Queue Jobs & Cron']
    },
    {
      title: 'Mobile & Frontend',
      items: ['Flutter & Dart', 'Android Studio', 'React & Astro.js', 'Tailwind & Bootstrap', 'Svelte & Vue basics', 'Responsive design']
    },
    {
      title: 'Database & Tools',
      items: ['MySQL & PostgreSQL', 'Firebase Auth & Firestore', 'Docker', 'Git & GitHub', 'Postman', 'DOKU Payments']
    },
    {
      title: 'Workflow & Design',
      items: ['Agile project management', 'Figma UI/UX', 'Obsidian & Notion', 'Technical documentation', 'Public speaking', 'Indonesian & English']
    }
  ];

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);

    const ctx = gsap.context(() => {
      gsap.from(cols, {
        scrollTrigger: {
          trigger: sectionEl,
          start: 'top 80%',
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

<section id="toolkit" bind:this={sectionEl} class="grid border-b hairline md:grid-cols-5">
  <div class="border-r hairline px-6 py-8 md:px-8">
    <p class="mono text-xs">07 / TOOLKIT</p>
  </div>
  <div class="col-span-4 grid sm:grid-cols-2 lg:grid-cols-4">
    {#each toolkits as toolkit, i}
      <article
        bind:this={cols[i]}
        class="border-b hairline px-6 py-8 {i % 2 === 0 ? 'sm:border-r' : ''} {i < 3 ? 'lg:border-r' : ''} lg:border-b-0 md:px-8"
      >
        <h3 class="mb-5 text-lg font-semibold">{toolkit.title}</h3>
        <p class="text-sm leading-8 opacity-60">
          {#each toolkit.items as item, itemIdx}
            {item}{#if itemIdx < toolkit.items.length - 1}<br />{/if}
          {/each}
        </p>
      </article>
    {/each}
  </div>
</section>
