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
        y: 25,
        opacity: 0,
        stagger: 0.12,
        duration: 0.75,
        ease: 'power2.out'
      });
    }, sectionEl);

    return () => ctx.revert();
  });
</script>

<section class="grid border-b hairline md:grid-cols-5" bind:this={sectionEl}>
  <div class="border-r hairline px-6 py-8 md:px-8">
    <p class="mono text-xs">06 / LEADERSHIP</p>
  </div>
  <div class="col-span-4 grid md:grid-cols-2">
    <article bind:this={articles[0]} class="border-b hairline px-6 py-7 md:border-b-0 md:border-r md:px-8">
      <h3 class="mb-2 text-xl font-medium">Workshop Riset Informatika</h3>
      <p class="mb-3 text-sm opacity-60">Head of Backend Division · Sep 2025 — Present</p>
      <p class="text-sm leading-relaxed opacity-60">
        Directing curriculum, coordinating mentors, and structuring backend development learning programs.
      </p>
    </article>

    <article bind:this={articles[1]} class="border-b hairline px-6 py-7 md:border-b-0 md:px-8">
      <h3 class="mb-2 text-xl font-medium">Technically Ramadhan</h3>
      <p class="mb-3 text-sm opacity-60">Event Lead · February 2026</p>
      <p class="text-sm leading-relaxed opacity-60">
        Led end-to-end execution, cross-divisional committee management, and post-event evaluation.
      </p>
    </article>

    <article bind:this={articles[2]} class="border-t hairline px-6 py-7 md:border-r md:px-8">
      <h3 class="mb-2 text-xl font-medium">Open Recruitment & Beta Class</h3>
      <p class="mb-3 text-sm opacity-60">Coordinator & Programming Mentor · 2025</p>
      <p class="text-sm leading-relaxed opacity-60">
        Taught programming fundamentals and coordinated selection logistics for incoming members.
      </p>
    </article>

    <article bind:this={articles[3]} class="border-t hairline px-6 py-7 md:px-8">
      <h3 class="mb-2 text-xl font-medium">Efwan Chapter & Bantengbalap.id</h3>
      <p class="mb-3 text-sm opacity-60">IT Support · Content Creator · 2026</p>
      <p class="text-sm leading-relaxed opacity-60">
        Supported live event systems and created motorsport graphics, reels, and structured content calendars.
      </p>
    </article>
  </div>
</section>
