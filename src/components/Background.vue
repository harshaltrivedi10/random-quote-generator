<template>
  <div id="background" :style="myStyle">
    <app-quote-container
      :bgColor="myStyle.backgroundColor"
      :quote="quote"
      :getQuote="getQuote"
      :href="href"
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
      },
      href: ""
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
          data.data[index].author.length != null
            ? (this.quote.author = data.data[index].author)
            : (this.quote.author = "Anonymous");
          this.href =
            "https://www.twitter.com/intent/tweet?text=" +
            '"' +
            this.quote.text +
            '"' +
            " -" +
            this.quote.author +
            "&hashtags=bigOnQuotes";
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
