<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  let sectionEl;
  let contactTitle;
  let contactDetails;
  let ovalContact;

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);

    const ctx = gsap.context(() => {
      gsap.from(contactTitle, {
        scrollTrigger: {
          trigger: sectionEl,
          start: 'top 75%',
          toggleActions: 'play none none none'
        },
        y: 40,
        opacity: 0,
        duration: 0.9,
        ease: 'power3.out'
      });

      gsap.from(contactDetails, {
        scrollTrigger: {
          trigger: sectionEl,
          start: 'top 70%',
          toggleActions: 'play none none none'
        },
        y: 25,
        opacity: 0,
        duration: 0.8,
        delay: 0.2,
        ease: 'power2.out'
      });

      // Subtle organic floating for contact decorative oval
      gsap.to(ovalContact, {
        y: -10,
        x: 6,
        rotation: 3,
        duration: 4.2,
        repeat: -1,
        yoyo: true,
        ease: 'sine.inOut'
      });
    }, sectionEl);

    return () => ctx.revert();
  });
</script>

<section id="contact" bind:this={sectionEl} class="hero-wash contact-height relative grid border-b hairline md:grid-cols-5">
  <div class="border-r hairline px-6 py-8 md:px-8">
    <p class="mono text-xs">08 / CONTACT</p>
  </div>
  <div class="relative col-span-4 flex flex-col justify-between px-6 py-12 md:px-8 md:py-16">
    <h2 bind:this={contactTitle} class="contact-title max-w-5xl font-medium leading-none">
      Let’s make<br />something useful.
    </h2>

    <div bind:this={contactDetails} class="flex flex-col justify-between gap-8 md:flex-row md:items-end">
      <div>
        <p class="mb-2 text-sm opacity-60">Available for internships, freelance projects, and collaborations.</p>
        <a class="text-lg underline underline-offset-4" href="mailto:faforite36@gmail.com">
          faforite36@gmail.com
        </a>
      </div>
      <div class="flex gap-5 text-sm">
        <a href="https://github.com/ItsNovaaa" target="_blank" rel="noopener noreferrer" class="hover:underline">
          GitHub ↗
        </a>
        <a href="https://wa.me/6281915862210" target="_blank" rel="noopener noreferrer" class="hover:underline">
          WhatsApp ↗
        </a>
        <a href="assets/CV_Naufal_Ramadhan.pdf" download class="hover:underline">
          CV ↓
        </a>
      </div>
    </div>

    <div
      bind:this={ovalContact}
      class="oval pointer-events-none absolute bottom-16 right-12 h-20 w-32 bg-white/50 md:h-28 md:w-48"
    ></div>
  </div>
</section>
