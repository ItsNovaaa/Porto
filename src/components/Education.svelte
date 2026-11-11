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
        y: 30,
        opacity: 0,
        stagger: 0.15,
        duration: 0.8,
        ease: 'power2.out'
      });
    }, sectionEl);

    return () => ctx.revert();
  });
</script>

<section class="grid border-b hairline md:grid-cols-5" bind:this={sectionEl}>
  <div class="border-r hairline px-6 py-8 md:px-8">
    <p class="mono text-xs">04 / EDUCATION</p>
  </div>
  <div class="col-span-4 grid md:grid-cols-2">
    <article bind:this={articles[0]} class="border-b hairline px-6 py-8 md:border-b-0 md:border-r md:px-8">
      <div class="mb-16 flex justify-between text-xs">
        <span class="mono">2024 — PRESENT</span>
        <span>GPA 3.67</span>
      </div>
      <h3 class="mb-2 text-2xl font-medium">Politeknik Negeri Malang</h3>
      <p class="mb-4 text-sm opacity-60">D4 Information Technology — Business Information Systems</p>
      <p class="text-sm leading-relaxed opacity-60">
        Focused on software engineering, distributed systems, and business technology workflows. Head of Backend Division at WRI Polinema.
      </p>
    </article>

    <article bind:this={articles[1]} class="px-6 py-8 md:px-8">
      <div class="mb-16 flex justify-between text-xs">
        <span class="mono">2021 — 2024</span>
        <span>GRADUATED</span>
      </div>
      <h3 class="mb-2 text-2xl font-medium">SMK Negeri 1 Boyolangu</h3>
      <p class="mb-4 text-sm opacity-60">Software Engineering</p>
      <p class="text-sm leading-relaxed opacity-60">
        Built a strong foundation in computer science, databases, algorithms, and application architecture through vocational study and freelance work.
      </p>
    </article>
  </div>
</section>
