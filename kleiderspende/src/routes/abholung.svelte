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
  const OFFICE_PREFIX = OFFICE.zip.slice(0, 2);

  let street = "";
  let zip = "";
  let city = "";
  let clothing = clothingTypes[0];
  let crisis = crisisAreas[0];

  let error = "";
  let tooFar = false; 

  function validate() {
    if (!street.trim() || !city.trim()) {
      error = "Bitte Straße und Ort ausfüllen.";
      tooFar = false;
      return false;
    }
    if (!/^\d{5}$/.test(zip)) {
      error = "Bitte gib eine gültige 5-stellige Postleitzahl ein.";
      tooFar = false;
      return false;
    }
    if (zip.slice(0, 2) !== OFFICE_PREFIX) {
      error = `Die Abholadresse liegt zu weit entfernt. Eine Abholung ist außerhalb des PLZ-Bereichs ${OFFICE_PREFIX} nicht möglich.`;
      tooFar = true;
      return false;
    }
    error = "";
    tooFar = false;
    return true;
  }

  function handleSubmit(e) {
    e.preventDefault();
    if (!validate()) return;

    const place = `${street}, ${zip} ${city}`;
    const ts = new Date().toISOString();

    push(
      `/bestaetigung?mode=abholung` +
        `&clothing=${encodeURIComponent(clothing)}` +
        `&crisis=${encodeURIComponent(crisis)}` +
        `&place=${encodeURIComponent(place)}` +
        `&ts=${encodeURIComponent(ts)}`
    );
  }
</script>

<section class="max-w-3xl mx-auto px-4 py-10 text-white">
  <h1 class="text-3xl md:text-4xl font-bold mb-3">
    Abholung des Sammelfahrzeugs
  </h1>
  <p class="text-lg opacity-90 mb-8">
    Bitte gib die <span class="font-semibold">Abholadresse</span> an und wähle
    die <span class="font-semibold">Art der Kleidung</span> sowie ein
    <span class="font-semibold">aktuelles Krisengebiet</span>.
  </p>

  {#if error}
    <div class="mb-4 rounded-lg bg-red-600/90 px-4 py-3">
      <p>{error}</p>
    </div>
  {/if}

  <form class="space-y-6" on:submit={handleSubmit} novalidate>
    <div>
      <label class="block mb-2 font-medium" for="street">Straße &amp; Nr.</label
      >
      <input
        id="street"
        bind:value={street}
        class="w-full rounded-lg bg-white text-black px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500"
        required
      />
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
      <div>
        <label class="block mb-2 font-medium" for="zip">PLZ</label>
        <input
          id="zip"
          bind:value={zip}
          class="w-full rounded-lg bg-white text-black px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500"
          inputmode="numeric"
          maxlength="5"
          required
        />
      </div>
      <div>
        <label class="block mb-2 font-medium" for="city">Ort</label>
        <input
          id="city"
          bind:value={city}
          class="w-full rounded-lg bg-white text-black px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500"
          required
        />
      </div>
    </div>

    <div>
      <label class="block mb-2 font-medium" for="clothing"
        >Art der Kleidung</label
      >
      <select
        id="clothing"
        bind:value={clothing}
        class="w-full rounded-lg bg-white text-black px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
        {#each clothingTypes as t}<option value={t}>{t}</option>{/each}
      </select>
    </div>

    <div>
      <label class="block mb-2 font-medium" for="crisis">Krisengebiet</label>
      <select
        id="crisis"
        bind:value={crisis}
        class="w-full rounded-lg bg-white text-black px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
        {#each crisisAreas as c}<option value={c}>{c}</option>{/each}
      </select>
    </div>

    <div class="flex justify-end gap-3 pt-2">
      <a
        href="#/auswahl"
        class="w-40 inline-flex items-center justify-center rounded-lg border border-white/40 bg-transparent px-6 py-3 font-semibold hover:bg-white/10 transition-colors text-center focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
        Zurück
      </a>

      <button
        type="submit"
        class="w-40 inline-flex items-center justify-center rounded-lg bg-indigo-600 hover:bg-indigo-700 px-6 py-3 font-semibold focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
        Registrieren
      </button>
    </div>
  </form>

  <p class="mt-6 text-sm opacity-80">
    Hinweis: Die ersten zwei Ziffern der PLZ müssen <strong
      >{OFFICE_PREFIX}</strong
    >
    entsprechen (Nähe zur Geschäftsstelle in {OFFICE.city}).
  </p>
</section>
