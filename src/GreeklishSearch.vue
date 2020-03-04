<template>
  <div>
    <input type="text" :value="txt" @input="greeklishToGreek" />
  </div>
</template>

<script>
let englishAcronymArray = new Array([
  "fb",
  "facebook",
  "twitter",
  "btw",
  "cu",
  "lol",
  "rofl",
  "wtf",
  "love u",
  "me 2",
  "ok",
  "OMFG",
  "OMG",
  "PLZ",
  "CYA",
  "LMAO",
  "LMFAO",
  "ROFLMAO",
  "BTW",
  "THX",
  "sms",
  "gay",
  "chat",
  "tweet",
  "twit",
  "twits",
  "pinterest",
  "FAIL",
  "linkedin",
  "epic",
  "tweets",
  "google",
  "like",
  "share",
  "face",
  "greeklish",
  "copy",
  "paste",
  "yahoo",
  "ebay",
  "amazon",
  "myspace",
  "youtube",
  "web",
  "http",
  "https",
  "cd",
  "dvd",
  "video",
  "mp3",
  "bf",
  "gf"
]);

let greeklishCharactersToGreekArray = {
  tha: "θα",
  the: "θε",
  thi: "θι",
  thh: "θη",
  tho: "θο",
  "(thy|thu)": "θυ",
  "(thw|thv)": "θω",
  tH: "τΗ",
  TH: "ΤΗ",
  Th: "Τη",
  th: "τη",
  "(cH|ch)": "χ",
  "(CH|Ch)": "Χ",
  "(PS|Ps)": "Ψ",
  "(ps|pS)": "ψ",
  "(Ks|KS)": "Ξ",
  "(ks|kS)": "ξ",
  "(VR)": "ΒΡ",
  "(vr|vR)": "βρ",
  "(Vr)": "Βρ",
  "8a": "θα",
  "8e": "θε",
  "8h": "θη",
  "8i": "θι",
  "8o": "θο",
  "8y": "θυ",
  "8u": "θυ",
  "(8v|8w)": "θω",
  "8A": "ΘΑ",
  "8E": "ΘΕ",
  "8H": "ΘΗ",
  "8I": "ΘΙ",
  "8O": "ΘΟ",
  "(8Y|8U)": "ΘΥ",
  "8V": "ΘΩ",
  "8W": "ΘΩ",
  "9a": "θα",
  "9e": "θε",
  "9h": "θη",
  "9i": "θι",
  "9o": "θο",
  "9y": "θυ",
  "9u": "θυ",
  "(9v|9w)": "θω",
  "9A": "ΘΑ",
  "9E": "ΘΕ",
  "9H": "ΘΗ",
  "9I": "ΘΙ",
  "9O": "ΘΟ",
  "(9Y|9U)": "ΘΥ",
  "9V": "ΘΩ",
  "9W": "ΘΩ",
  "s[\\n]": "ς\n",
  "s[\\!]": "ς!",
  "s[\\.]": "ς.",
  "s[\\ ]": "ς ",
  "s[\\,]": "ς,",
  "s[\\\\+]": "ς+",
  "s[\\-]": "ς-",
  "s[\\(]": "ς(",
  "s[\\)]": "ς)",
  "s[\\[]": "ς[",
  "s[\\]]": "ς]",
  "s[\\{]": "ς{",
  "s[\\}]": "ς}",
  "s[\\<]": "ς<",
  "s[\\>]": "ς>",
  "s[\\?]": "ς?",
  "s[\\/]": "ς/",
  "s[\\:]": "ς:",
  "s[\\;]": "ς;",
  's[\\"]': 'ς"',
  "s[\\']": "ς'",
  "s[\\f]": "ς\f",
  "s[\\r]": "ς\r",
  "s[\\t]": "ς\t",
  "s[\\v]": "ς\\v",
  rx: "ρχ",
  sx: "σχ",
  Sx: "Σχ",
  SX: "ΣΧ",
  ux: "υχ",
  Ux: "Υχ",
  UX: "ΥΧ",
  yx: "υχ",
  Yx: "Υχ",
  YX: "ΥΧ",
  "3a": "ξα",
  "3e": "ξε",
  "3h": "ξη",
  "3i": "ξι",
  "3ο": "ξο",
  "3u": "ξυ",
  "3y": "ξυ",
  "3v": "ξω",
  "3w": "ξω",
  a3: "αξ",
  e3: "εξ",
  h3: "ηξ",
  i3: "ιξ",
  ο3: "οξ",
  u3: "υξ",
  y3: "υξ",
  v3: "ωξ",
  w3: "ωξ",
  "3A": "ξΑ",
  "3E": "ξΕ",
  "3H": "ξΗ",
  "3I": "ξΙ",
  "3O": "ξΟ",
  "3U": "ξΥ",
  "3Y": "ξΥ",
  "3V": "ξΩ",
  "3W": "ξΩ",
  A3: "Αξ",
  E3: "Εξ",
  H3: "Ηξ",
  I3: "Ιξ",
  O3: "Οξ",
  U3: "Υξ",
  Y3: "Υξ",
  V3: "Ωξ",
  W3: "Ωξ",
  A: "Α",
  a: "α",
  B: "Β",
  b: "β",
  V: "Β",
  v: "β",
  c: "ψ",
  C: "Ψ",
  G: "Γ",
  g: "γ",
  D: "Δ",
  d: "δ",
  E: "Ε",
  e: "ε",
  Z: "Ζ",
  z: "ζ",
  H: "Η",
  h: "η",
  U: "Θ",
  u: "υ",
  I: "Ι",
  i: "ι",
  j: "ξ",
  J: "Ξ",
  K: "Κ",
  k: "κ",
  L: "Λ",
  l: "λ",
  M: "Μ",
  m: "μ",
  N: "Ν",
  n: "ν",
  X: "Χ",
  x: "χ",
  O: "Ο",
  o: "ο",
  P: "Π",
  p: "π",
  R: "Ρ",
  r: "ρ",
  S: "Σ",
  s: "σ",
  T: "Τ",
  t: "τ",
  Y: "Υ",
  y: "υ",
  F: "Φ",
  f: "φ",
  W: "Ω",
  w: "ω"
};

// let greeklishWordsTogreekArray = {
// 	"\\bre\\ c\\b" : "ρε συ",
// 	"\\btpt\\b" : "τίποτα",
// 	"\\bdn\\b" : "δεν",
// 	"\\bd\\b" : "δεν",
// 	"\\bm\\b" : "μου/με",
// 	"\\bs\\b" : "σου/σε",
// 	"\\bn\\b" : "να",
// 	"\\btr\\b" : "τώρα",
// 	"\\bsmr\\b" : "σήμερα",
// 	"\\bklmr\\b" : "καλημέρα",
// 	"\\bklnx\\b" : "καληνύχτα",
// 	"\\bklnxt\\b" : "καληνύχτα",
// 	"\\btlm\\b" : "τα λέμε",
// 	"\\bsks\\b" : "σκάσε",
// 	"\\bkn1\\b" : "κανένα",
// 	"\\bdld\\b" : "δηλαδή",
// 	"\\bvrm\\b" : "βαριέμαι",
// 	"\\bmlk\\b" : "μαλάκα",
// 	"\\bmlks\\b" : "μαλάκας/μαλακία",
// 	"\\bmlkies\\b" : "μαλακίες",
// 	"\\b(mnm|mna|mn)\\b" : "μήνυμα",
// 	"\\bgt\\b" : "γιατί",
// 	"\\btespa\\b" : "τέλος πάντων",
// 	"\\btes\\ pa\\b" : "τέλος πάντων",
// 	"\\b(til|thl)\\b" : "τηλέφωνο",
// 	"\\btn\\b" : "τον/την",
// 	"\\+fono\\b" : "συμφωνώ",
// 	"\\bk\\b" : "και",
// 	"\\bi\\b" : "η",
// 	"\\bg\\b" : "για",
// 	"\\bt\\b" : "το/τα/τη/τι",
// 	"\\bth\\b" : "θα",
// 	"\\bine\\b" : "είναι",
// 	"\\bime\\b" : "είμαι",
// 	"\\bakm\\b" : "ακόμα",
// 	"\\banap\\b" : "αναπάντητη",
// 	"\\betc\\b" : "έτσι",
// 	"\\bflk\\b" : "φιλάκια",
// 	"\\bgmt\\b" : "γαμώτο",
// 	"\\bgt\\b" : "γιατί",
// 	"\\bkl\\b" : "καλά",
// 	"\\bknt\\b" : "κινητό",
// 	"\\bkt\\b" : "κάτι",
// 	"\\blps\\b" : "λείπεις",
// 	"\\bmt\\b" : "μετά",
// 	"\\bn\\b" : "να",
// 	"\\bnmz\\b" : "νομίζω",
// 	"\\botn\\b" : "όταν",
// 	"\\bp\\b" : "που",
// 	"\\bpx\\b" : "π.χ.",
// 	"\\br\\b" : "ρε",
// 	"\\bsk\\b" : "Σ/Κ",
// 	"\\bspt\\b" : "σπίτι",
// 	"\\bsxl\\b" : "σχολή/σχολείο",
// 	"\\bt\\b" : "το/τα",
// 	"\\bts\\b" : "της/τις",
// 	"\\bkns\\b" : "κάνεις",
// 	"\\blm\\b" : "λέμε",
// 	"\\btpt\\b" : "τίποτα",
// 	"\\bbsk\\b" : "βασικά",
// 	"\\bfcka\\b" : "φυσικά",
// 	"\\bgnt\\b" : "γίνετε",
// 	"\\bitn\\b" : "ήταν",
// 	"\\bkpn\\b" : "κάποιον",
// 	"\\bktlvs\\b" : "κατάλαβες",
// 	"\\blpn \\b" : "λοιπόν",
// 	"\\bmn\\b" : "μην",
// 	"\\bplk\\b" : "πλάκα",
// 	"\\bprp\\b" : "πρέπει",
// 	"\\bpt\\b" : "πότε",
// 	"\\b8l\\b" : "θέλω",
// 	"\\btr\\b" : "τώρα",
// 	"\\bbb\\b" : "bye bye",
// 	"\\bplz \\b" : "παρακαλώ",
// 	"\\bpic\\b" : "εικόνα"
// }

import jQuery from "jquery";
const $ = jQuery;
window.$ = $;

export default {
  name: "GreeklishSearch",
  props: ["value"],
  computed: {
    englishAcronym() {
      return englishAcronymArray;
    },
    // greeklishWordsTogreek() {
    //   return greeklishWordsTogreekArray;
    // },
    greeklishCharactersToGreek() {
      return greeklishCharactersToGreekArray;
    }
  },
  data() {
    return {
      txt: null
    };
  },
  methods: {
    greeklishToGreek(e) {
      let greeklishText = e.target.value;

      var words = new Array();
      var wordsCounter = 1000;

      $.each(englishAcronymArray, function(key, value) {
        // perform global case-insesitive march using gi modifier and match
        // whole words using \b metacharacter
        // more info here
        // http://www.regular-expressions.info/wordboundaries.html
        greeklishText = greeklishText.replace(
          RegExp("\\b" + value + "\\b", "gi"),
          "*&$" + wordsCounter + "^&*"
        );
        wordsCounter++;
        words.push(value);
      });

      //   $.each(greeklishWordsTogreekArray, function(key, value) {
      //     // perform global case-insesitive march using gi modifier
      //     greeklishText = greeklishText.replace(RegExp(key, "gi"), value);
      //   });

      $.each(greeklishCharactersToGreekArray, function(key, value) {
        // perform global march using g modifier
        greeklishText = greeklishText.replace(RegExp(key, "g"), value);
      });

      // replace the number with the english words
      $.each(words, function(index, value) {
        greeklishText = greeklishText.replace(
          RegExp("\\*\\&\\$" + (1000 + index) + "\\^\\&\\*", "gi"),
          value
        );
      });
      console.log(greeklishText);
      this.$emit("input", greeklishText);
      // this.txt = greeklishText;
    }
  }
};
</script>