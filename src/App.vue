<template>
  <div class="gradientbg" :class="cardActive ? 'opaquebg' : ''">
    <div class="container">
      <div class="row">
        <div
          v-for="c in content"
          :key="c"
          :class="
            c.active == true && c.type == 'ExpandCard' ? 'col-12' : c.columns
          "
        >
          <div
            class="customcard"
            :class="
              c.type == 'Headline' || c.active == true ? c.class : 'closed '
            "
            @click="c.type !== 'Headline' ? activate(c) : ''"
          >
            <h4>{{ c.subline }}</h4>
            <div v-if="c.type == 'Headline' || c.active == true">
              <div v-if="c.hasOwnProperty('text')">{{ c.text }}</div>
              <div v-if="c.hasOwnProperty('bullets')">
                <ul>
                  <li v-for="bullet in c.bullets" :key="bullet" class="bullet">
                    {{ bullet }}
                  </li>
                </ul>
              </div>
              <div v-if="c.hasOwnProperty('ordered')">
                <ol>
                  <li v-for="bullet in c.ordered" :key="bullet" class="bullet">
                    {{ bullet }}
                  </li>
                </ol>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      content: [
        {
          text: "Frontend for Noobs",
          class: "headline",
          columns: "col-12",
          type: "Headline",
        },
        {
          subline: "Was macht dieses Frontend?",
          bullets: [
            "Empfängt Daten und Code aus dem Backend",
            "Stellt dem Nutzer die Daten in ansprechender und geordneter Form dar",
            "Ermöglicht Nutzer-Input",
            "Überprüft und sendet Nutzer-Input ans Backend",
          ],
          class: "basic",
          columns: "col-12 col-md-6",
          type: "ExpandCard",
          active: false,
        },
        {
          subline: "Frontend vs. Backend vs. Infra",
          bullets: [
            "Frontend: Code wird im Browser auf dem Gerät des Nutzers ausgeführt, ist editierbar, Änderungen werden beim neu Laden verworfen.",
            "Backend: Stellt den Frontend Code bereit, läuft auf dem Server, ist nicht vom Nutzer einsehbar, empfängt Input aus dem Frontend, validiert ihn und arbeitet damit. Kommuniziert mit der Datenbank",
            "Infra: Kümmert sich um Server- und Datenbankprovider, verschiedene Sicherheitsaspekte, etc.",
          ],
          class: "fancy",
          columns: "col-12 col-md-6",
          type: "ExpandCard",
          active: false,
        },
        {
          subline: "HTML",
          bullets: [
            "steht für Hypertext Markup Language",
            "stellt Text und andere Elemente strukturiert dar",
          ],
          class: "html",
          columns: "col-12 col-md-4",
          type: "Card",
          active: false,
        },
        {
          subline: "CSS",
          bullets: [
            "ermöglicht umfangreiches Styling für html elemente",
            "entscheidend für responsive Websites",
          ],
          class: "css",
          columns: "col-12 col-md-4",
          type: "Card",
          active: false,
        },
        {
          subline: "Javascript",
          bullets: [
            "fügt Funktionalität hinzu:",
            "Für den Nutzer sichtbar: Buttons, Input Felder, etc..",
            "im Hintergrund: Schleifen, Konditionen, Kommunikation mit Backend/API's",
          ],
          class: "basic",
          columns: "col-12 col-md-4",
          type: "Card",
          active: false,
        },
        {
          subline: "Vue",
          bullets: [
            "Frontend Framework:",
            'spezielle "Schreibweise" für HTML/CSS/JS',
            "hat viele Funktionalitäten integriert",
            "optimiert die Seite in Bezug auf Datenmengen, Ladegeschwindigkeit bei Änderungen",
          ],
          class: "basic",
          columns: "col-12 col-md-4",
          type: "ExpandCard",
          active: false,
        },
        {
          subline: "Modularität",
          bullets: [
            "Einer der Hauptgründe für Frameworks",
            "Entwickler schreiben Vorlagen/Skelette, die mit verschiedenen Informationen gefüllt werden",
            "Reduziert die Menge an Code enorm, macht Wartung und Änderungen viel schneller",
          ],
          class: "basic",
          columns: "col-12 col-md-4",
          type: "ExpandCard",
          active: false,
        },
        {
          subline: "Bootstrap & DPL",
          bullets: [
            "Bootstrap: Vorgefertige CSS&JS Bausteine, um schnell und einheitlich Seiten zu erstellen. Macht responsive Layouts viel einfacher.",
            "DPL: unser angepasstes Bootstrap mit den DCA Farben, Schriftarten. Single Source of Truth für styling. ",
          ],
          class: "basic",
          columns: "col-12 col-md-4",
          type: "ExpandCard",
          active: false,
        },

        {
          text: "WTF is a Pull Request",
          class: "headline",
          columns: "col-12",
          type: "Headline",
        },
        {
          subline: "Github",
          bullets: [
            "Git: System zur Versionskontrolle, speichert und verwaltet Änderungen an Dokumenten.",
            "Github: Online Service, um mit Git Versionskontrolle durchzuführen.",
            "Codesharing Platform.",
          ],
          class: "basic",
          columns: "col-12",
          type: "ExpandCard",
          active: false,
        },
        {
          subline: "Der gute Git Prozess",
          ordered: [
            "Ich erstelle einen neuen Branch vom Hauptbranch aus.",
            "Ich mache meine Änderungen.",
            'Ich "pushe" meine Änderungen auf Github und stelle einen Pull Request',
            "Ein anderer Entwickler überprüft meine Änderungen und approved den Pull Request",
            'Ich "pulle" meine Änderungen zurück auf den Hauptbranch',
            "Der Hauptbranch ist jetzt auf dem aktuellsten Stand.",
            "Ich kann meinen Branch löschen.",
          ],
          class: "basic",
          columns: "col-12 col-md-6",
          type: "Card",
          active: false,
        },
        {
          subline: "Der weniger Gute",
          ordered: [
            "Ich erstelle einen neuen Branch vom Hauptbranch aus.",
            "Tobi erstellt auch einen neuen Branch vom Hauptbranch aus.",
            "Ich mache Änderungen an Zeile 10-20 im Dokument App.vue.",
            "Tobi ändert auch Zeile 10-20 in App.vue.",
            "Tobi merged seinen Branch auf den Hauptbranch.",
            "Der Hauptbranch enthält jetzt Tobi's Änderungen",
            "Wenn ich meine Änderungen mergen möchte, muss ich händisch überprüfen, welche von Tobi's und welche von meinen Änderungen übernommen werden sollen.",
          ],
          class: "fancy",
          columns: "col-12 col-md-6",
          type: "Card",
          active: false,
        },
        {
          subline: "Wie läuft eine Code Review",
          bullets: [
            "Vor jedem merge muss der Code von mindestens einem Team Mitglied geprüft und approved werden.",
            "Geprüft wird auf Effizienz und Lesbarkeit des Code und die Funktionalität in allen Endbrowsern wird getestet.",
            "Nach der Code Review macht Nicola noch eine Style Review und Browser Tests.",
          ],
          class: "basic",
          columns: "col-12",
          type: "ExpandCard",
          active: false,
        },

        {
          text: "Speed Round",
          class: "headline",
          columns: "col-12",
          type: "Headline",
        },
        {
          subline: "Stackoverflow",
          text:
            "Forum für alle Developer Fragen, meistens das erste Google Suchergebnis.",
          class: "basic",
          columns: "col-12 col-md-6",
          type: "Card",
          active: false,
        },
        {
          subline: "Cron Job",
          text:
            "Automatisierter Task im Backend, der in einem festgelegten Zeitabstand wiederholt wird.",
          class: "basic",
          columns: "col-12 col-md-6",
          type: "Card",
          active: false,
        },
        {
          subline: "Refactoring",
          text:
            "Code umschreiben/optimieren, ohne das sich das Endprodukt ändert.",
          class: "basic",
          columns: "col-12 col-md-6",
          type: "Card",
          active: false,
        },
        {
          subline: "Gibt die API ein JSON zurück?",
          text:
            "Hängt von der API ab, heute meistens schon. JSON ist ein Format, in dem Javascript Objekte gespeichert werden.",
          class: "basic",
          columns: "col-12 col-md-6",
          type: "Card",
          active: false,
        },
        {
          subline: "Vielen Dank für eure Aufmerksamkeit",
          text: "Welche Fragen habt ihr noch?",
          class: "basic",
          columns: "col-12",
          type: "Card",
          active: false,
        },
      ],
    };
  },
  computed: {
    cardActive() {
      let res = false;
      this.content.map((c) => {
        if (c.active == true) {
          res = true;
        }
      });
      return res;
    },
  },
  methods: {
    activate(x) {
      this.content
        .filter((c) => c == x)
        .map((c) => {
          c.active = !c.active;
          if (!c.class.includes("active")) {
            c.class += " active";
          } else {
            c.class = c.class.slice(0, c.class.length - 7);
          }
          return c;
        });
    },
  },
};
</script>

<style>
.opaquebg {
  background-color: rgba(68, 72, 99, 0.5);
  z-index: 1;
}
.gradientbg {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
}
.customcard {
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(5px);
  border-radius: 4px;
  margin-bottom: 16px;
  padding: 16px;
}
.closed {
  text-align: center;
  padding-top: 16px;
  padding-bottom: 16px;
}
.active {
  background-color: rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(5px);
  z-index: 10;
}
.headline {
  border: none;
  background: none !important;
  font-size: 300%;
  font-weight: bold;
  margin-top: 32px;
  margin-left: -16px;
}
.html {
  font-family: "Times New Roman", Times, serif;
  border-radius: 0;
  background-color: white;
}

.bullet {
  padding-bottom: 1rem;
  font-size: 120%;
}
</style>
