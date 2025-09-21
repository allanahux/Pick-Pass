<script>
  import { push } from "svelte-spa-router";

  const clothingTypes = [
    "Kinderkleidung",
    "Damenkleidung",
    "Herrenbekleidung",
    "Jacken/Mäntel",
    "Schuhe",
    "Decken",
  ];
  const crisisAreas = ["Ukraine", "Syrien", "Jemen", "Sudan"];
  const OFFICE = {
    name: "Pick & Pass Geschäftsstelle",
    street: "Musterstraße 1",
    zip: "10115",
    city: "Berlin",
  };

  let clothing = clothingTypes[0];
  let crisis = crisisAreas[0];

  function handleSubmit(e) {
    e.preventDefault();
    const place = `${OFFICE.name}, ${OFFICE.street}, ${OFFICE.zip} ${OFFICE.city}`;
    const ts = new Date().toISOString();

    push(
      `/bestaetigung?mode=abgabe` +
        `&clothing=${encodeURIComponent(clothing)}` +
        `&crisis=${encodeURIComponent(crisis)}` +
        `&place=${encodeURIComponent(place)}` +
        `&ts=${encodeURIComponent(ts)}`
    );
  }
</script>

<section class="max-w-3xl mx-auto px-4 py-10 text-white">
  <h1 class="text-3xl md:text-4xl font-bold mb-3">
    Abgabe an der Geschäftsstelle
  </h1>
  <p class="text-lg opacity-90 mb-8">
    Bitte wähle die <span class="font-semibold">Art der Kleidung</span> und ein
    <span class="font-semibold">aktuelles Krisengebiet</span>.
  </p>

  <form class="space-y-6" on:submit={handleSubmit}>
    <div>
      <label class="block mb-2 font-medium" for="clothing"
        >Art der Kleidung</label
      >
      <select
        id="clothing"
        bind:value={clothing}
        class="w-full rounded-lg bg-white text-black px-4 py-3"
      >
        {#each clothingTypes as t}
          <option value={t}>{t}</option>
        {/each}
      </select>
    </div>

    <div>
      <label class="block mb-2 font-medium" for="crisis">Krisengebiet</label>
      <select
        id="crisis"
        bind:value={crisis}
        class="w-full rounded-lg bg-white text-black px-4 py-3"
      >
        {#each crisisAreas as c}
          <option value={c}>{c}</option>
        {/each}
      </select>
    </div>

    <div class="flex justify-end gap-3 pt-2">
      <!-- Secondary Button -->
      <button
        type="button"
        class="w-40 inline-flex items-center justify-center rounded-lg border border-white/40 bg-transparent px-6 py-3 font-semibold hover:bg-white/10 transition-colors text-center focus:outline-none focus:ring-2 focus:ring-indigo-500"
        on:click={() => (window.location.hash = "/auswahl")}
      >
        Zurück
      </button>
      <!-- Primary Button -->
      <button
        type="submit"
        class="w-40 inline-flex items-center justify-center rounded-lg bg-indigo-600 hover:bg-indigo-700 px-6 py-3 font-semibold"
      >
        Registrieren
      </button>
    </div>
  </form>
</section>
