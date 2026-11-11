<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  let sectionEl;
  let articles = [];

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);

    const ctx = gsap.context(() => {
      gsap.from(articles, {
        scrollTrigger: {
          trigger: sectionEl,
          start: 'top 80%',
          toggleActions: 'play none none none'
        },
        y: 35,
        opacity: 0,
        stagger: 0.15,
        duration: 0.8,
        ease: 'power2.out'
      });
    }, sectionEl);

    return () => ctx.revert();
  });
</script>

<section id="about" bind:this={sectionEl} class="grid border-b hairline md:grid-cols-5">
  <div class="border-r hairline px-6 py-8 md:px-8">
    <p class="mono text-xs">02 / CAPABILITIES</p>
  </div>
  <div class="col-span-4 grid md:grid-cols-3">
    <article bind:this={articles[0]} class="border-b hairline px-6 py-8 md:border-b-0 md:border-r md:px-8">
      <p class="mono mb-14 text-xs">01</p>
      <h3 class="mb-3 text-xl font-semibold">Fullstack web</h3>
      <p class="text-sm leading-relaxed opacity-60">
        Laravel, Next.js, React, Astro, REST APIs, WebSockets, Docker, and databases.
      </p>
    </article>

    <article bind:this={articles[1]} class="border-b hairline px-6 py-8 md:border-b-0 md:border-r md:px-8">
      <p class="mono mb-14 text-xs">02</p>
      <h3 class="mb-3 text-xl font-semibold">Mobile products</h3>
      <p class="text-sm leading-relaxed opacity-60">
        Cross-platform Flutter applications, Android systems, OCR utilities, and Firebase.
      </p>
    </article>

    <article bind:this={articles[2]} class="px-6 py-8 md:px-8">
      <p class="mono mb-14 text-xs">03</p>
      <h3 class="mb-3 text-xl font-semibold">Team leadership</h3>
      <p class="text-sm leading-relaxed opacity-60">
        Project management, sprint planning, Git workflows, mentoring, and delivery.
      </p>
    </article>
  </div>
</section>
