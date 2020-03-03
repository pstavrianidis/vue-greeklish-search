<template>
  <div>
    <input type="text" :value="txt" @input="greeklishToGreek" />
  </div>
</template>

<script>
import englishAcronymArray from "./englishAcronymArray.json";
import greeklishWordsTogreekArray from "./greeklishWordsTogreekArray.json";
import greeklishCharactersToGreekArray from "./greeklishCharactersToGreekArray.json";

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
    greeklishWordsTogreek() {
      return greeklishWordsTogreekArray;
    },
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
    }
  }
};
</script>