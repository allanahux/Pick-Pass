<script>
  import { querystring } from "svelte-spa-router";

  $: params = new URLSearchParams($querystring || "");
  $: clothing = params.get("clothing");
  $: crisis = params.get("crisis");
  $: place = params.get("place");
  $: ts = params.get("ts");

  function splitDT(iso) {
    const d = new Date(iso);
    return {
      date: d.toLocaleDateString("de-DE", {
        year: "numeric",
        month: "2-digit",
        day: "2-digit",
      }),
      time: d.toLocaleTimeString("de-DE", {
        hour: "2-digit",
        minute: "2-digit",
      }),
    };
  }

  $: dt = splitDT(ts);
</script>

<section class="max-w-3xl mx-auto px-4 py-10 text-white">
  <h1 class="text-3xl md:text-4xl font-bold mb-3">Registrierung bestätigt</h1>
  <p class="opacity-90 mb-8">
    Deine Registrierung wurde erfolgreich <strong
      >unter Angabe aller Daten (Art der Kleider, Krisengebiet, Datum, Uhrzeit
      und Ort)</strong
    > bestätigt.
  </p>

  <div class="space-y-3 bg-white/10 backdrop-blur rounded-xl p-5">
    <div>
      <span class="opacity-80">Art der Kleider:</span>
      <strong>{clothing}</strong>
    </div>
    <div>
      <span class="opacity-80">Krisengebiet:</span> <strong>{crisis}</strong>
    </div>
    <div><span class="opacity-80">Datum:</span> <strong>{dt.date}</strong></div>
    <div>
      <span class="opacity-80">Uhrzeit:</span> <strong>{dt.time} Uhr</strong>
    </div>
    <div><span class="opacity-80">Ort:</span> <strong>{place}</strong></div>
  </div>

  <div class="flex justify-end gap-3 mt-8">
    <a
      href="#/"
      class="inline-flex items-center justify-center rounded-lg border border-white/30 bg-transparent px-6 py-3 font-semibold hover:bg-white/10"
    >
      Zurück zur Startseite
    </a>
  </div>
</section>
