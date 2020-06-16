<template>
  <div id="background" v-if="true" :style="myStyle">
    <app-quote-container
      :backgroundColor="myStyle.backgroundColor"
      :quote="quote"
      :getQuote="getQuote"
    ></app-quote-container>
  </div>
</template>

<script>
import QuoteContainer from "./QuoteContainer.vue";
import axios from "axios";
export default {
  name: "Background",
  components: {
    appQuoteContainer: QuoteContainer
  },
  data() {
    return {
      myStyle: {
        backgroundColor: ""
      },
      quote: {
        text: "",
        author: ""
      }
    };
  },
  created() {
    // this.myStyle.backgroundColor =
    //   "#" + Math.floor(Math.random() * 16777215).toString(16);
    this.getQuote();
  },
  methods: {
    getQuote() {
      this.myStyle.backgroundColor =
        "#" + Math.floor(Math.random() * 16777215).toString(16);
      console.log(this.myStyle.backgroundColor);
      const config = {
        headers: {
          "Access-Control-Allow-Origin": "*"
        },
        data: {}
      };
      axios
        .get(
          "https://cors-anywhere.herokuapp.com/https://type.fit/api/quotes",
          config
        )
        .then(data => {
          const index = Math.floor(Math.random() * 1600);
          console.log(data.data[index]);
          this.quote.text = data.data[index].text;
          this.quote.author = data.data[index].author;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
#background {
  height: 100vh;
}
</style>
