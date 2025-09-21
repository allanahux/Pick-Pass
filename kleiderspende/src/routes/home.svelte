<script>
  import { push } from "svelte-spa-router";
</script>

<div class="min-h-screen flex flex-col w-full">
  <!-- Content Bereich -->
  <main class="flex-1 flex flex-col items-center text-center pt-16">
    <!-- Hero-Bereich -->
    <section
      class="flex flex-col items-center justify-center min-h-[calc(100vh-4rem)] px-4 sm:px-6 lg:px-8 space-y-6"
    >
      <h2
        class="font-mono text-2xl sm:text-3xl md:text-5xl font-bold text-white"
      >
        Pick your Donation. Pass your Clothes.
      </h2>

      <p class="text-base sm:text-lg md:text-xl text-white max-w-xl">
        Schenke deinen Klamotten ein zweites Leben und helfe Menschen in Not.
      </p>

      <button
        class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-8 rounded-lg transition-colors"
        on:click={() => push("/auswahl")}
      >
        Jetzt spenden
      </button>

      <!-- Pfeil + So funktioniert’s -->
      <div class="flex flex-col items-center mt-10">
        <a
          href="#prozess"
          class="text-xl font-medium text-white mb-3 underline underline-offset-4 hover:text-indigo-300"
        >
          So funktioniert's.
        </a>
        <a href="#prozess">
          <img
            src="/arrow-down.svg"
            alt="Pfeil nach unten"
            class="w-10 h-20 animate-bounce"
          />
        </a>
      </div>
    </section>

    <section
      id="prozess"
      class="scroll-mt-28 sm:scroll-mt-32 md:scroll-mt-40 mt-24 pt-12 sm:pt-16 md:pt-20 pb-16 text-white"
    >
      <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">

        <h2
          class="font-mono text-2xl sm:text-3xl md:text-4xl font-bold text-center mb-12"
        >
          Deine Kleiderspende. <br /> Schritt-für-Schritt erklärt.
        </h2>

        <div class="space-y-8">

          <div class="flex flex-col md:flex-row md:items-center gap-4">
            <div
              class="flex-shrink-0 w-12 h-12 flex items-center justify-center bg-indigo-600 text-white font-bold rounded-full"
            >
              1
            </div>
            <p>
              Klicke auf <span class="font-semibold">Jetzt spenden</span> und
              wähle aus, ob deine Spende
              <span class="font-semibold">abgeholt</span>
              werden soll (Sammelfahrzeug kommt zu dir) oder ob du sie selbst
              <span class="font-semibold">vor Ort</span> abgibst.
            </p>
          </div>

          <div class="flex flex-col md:flex-row md:items-center gap-4">
            <div
              class="flex-shrink-0 w-12 h-12 flex items-center justify-center bg-indigo-600 text-white font-bold rounded-full"
            >
              2
            </div>
            <p>
              Fülle das kurze Formular aus und wähle die
              <span class="font-semibold">Krisenregion</span> aus, an die du spenden
              möchtest.
            </p>
          </div>

          <div class="flex flex-col md:flex-row md:items-center gap-4">
            <div
              class="flex-shrink-0 w-12 h-12 flex items-center justify-center bg-indigo-600 text-white font-bold rounded-full"
            >
              3
            </div>
            <p>Deine Registrierung wird bestätigt.</p>
          </div>

          <div class="flex flex-col md:flex-row md:items-center gap-4">
            <div
              class="flex-shrink-0 w-12 h-12 flex items-center justify-center bg-indigo-600 text-white font-bold rounded-full"
            >
              4
            </div>
            <p>
              Deine Spende wird entgegengenommen, sortiert und an bedürftige
              Menschen weitergegeben.
            </p>
          </div>
        </div>
      </div>
    </section>
  </main>
</div>
