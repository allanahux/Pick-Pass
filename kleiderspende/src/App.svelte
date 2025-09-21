<script>
  import Router, { push } from "svelte-spa-router";

  import Home from "./routes/home.svelte";
  import Auswahl from "./routes/auswahl.svelte";
  import Abgabe from "./routes/abgabe.svelte";
  import Abholung from "./routes/abholung.svelte";
  import Bestaetigung from "./routes/bestaetigung.svelte";
  import Impressum from "./routes/impressum.svelte";
  import Datenschutz from "./routes/datenschutz.svelte";
  import AGB from "./routes/agb.svelte";
  import NotFound from "./routes/notFound.svelte";

  const routes = {
    "/": Home,
    "/auswahl": Auswahl,
    "/abgabe": Abgabe,
    "/abholung": Abholung,
    "/bestaetigung": Bestaetigung,
    "/impressum": Impressum,
    "/datenschutz": Datenschutz,
    "/agb": AGB,
    "*": NotFound,
  };

  let menuOpen = false;

  const navLinks = [
    { name: "Jetzt spenden", path: "/auswahl" },
    { name: "Über uns", path: "/notFound" },
  ];
</script>

<svelte:head>
  <title>Pick & Pass - Deine Kleiderspende</title>
</svelte:head>

<!-- Header -->
<header class="fixed top-0 left-0 w-full bg-indigo-800 text-white z-50">
  <div class="mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
    <div class="flex h-16 items-center justify-between">
      <!-- Logo + Titel -->
      <a
        href="/"
        on:click|preventDefault={() => push("/")}
        class="flex items-center gap-5"
      >
        <img src="/logo.svg" alt="Pick & Pass Logo" class="h-10 w-10" />
        <span class="font-mono text-lg font-bold">Pick & Pass</span>
      </a>

      <!-- Navigation -->
      <nav class="flex gap-6 sm:gap-8">
        {#each navLinks as link (link.path)}
          <a
            href={link.path}
            on:click|preventDefault={() => push(link.path)}
            class="text-white font-bold rounded-lg px-3 py-2 hover:bg-indigo-300/30 transition-colors"
          >
            {link.name}
          </a>
        {/each}
      </nav>
    </div>
  </div>
</header>

<!-- SPA Router -->
<main>
  <Router {routes} />
</main>

<div aria-hidden="true" class="h-[80px] sm:h-[88px]"></div>

<footer class="fixed inset-x-0 bottom-0 z-40 bg-indigo-800 text-gray-300">
  <div
    class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8
    py-5 sm:py-6 text-sm md:text-base
    flex flex-col sm:flex-row justify-between items-center gap-3 sm:gap-6"
  >
    <nav class="flex flex-col sm:flex-row gap-3 sm:gap-6">
      <a 
        href="#/impressum" 
        on:click|preventDefault={() => push('/impressum')} 
        class="hover:text-white transition-colors"
      >
        Impressum
      </a>
      <a 
        href="#/datenschutz" 
        on:click|preventDefault={() => push('/datenschutz')} 
        class="hover:text-white transition-colors"
      >
        Datenschutz
      </a>
      <a 
        href="#/agb" 
        on:click|preventDefault={() => push('/agb')} 
        class="hover:text-white transition-colors"
      >
        AGB
      </a>
    </nav>

    <div class="text-center sm:text-right">
      © {new Date().getFullYear()} Pick & Pass. Alle Rechte vorbehalten.
    </div>
  </div>
</footer>

