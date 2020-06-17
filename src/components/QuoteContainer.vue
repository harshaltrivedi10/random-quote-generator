<template>
  <div id="quote-box">
    <div class="quote-text">
      <i class="fa fa-quote-left" :style="textStyle" id="quotation"></i>
      <span id="text" :style="textStyle">{{ quote.text }}</span>
    </div>
    <div class="quote-author">
      <span id="author" :style="textStyle">- {{ quote.author }}</span>
    </div>
    <div class="buttons">
      <div id="tweet-quote" :style="myStyle">
        <a :href="href" target="_blank">
          <i style="margin: 4px; font-size:24px; color: white" class="fa">
            &#xf099;
          </i>
        </a>
      </div>
      <button
        id="new-quote"
        class="btn btn-primary"
        :style="myStyle"
        @click="getQuote()"
      >
        New Quote
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "QuoteContainer",
  data() {
    return {
      myStyle: {
        backgroundColor: this.bgColor
      },
      textStyle: {
        color: this.bgColor
      }
    };
  },
  props: {
    bgColor: {
      type: String,
      required: true
    },
    href: {
      type: String,
      required: true
    },
    quote: {
      type: Object,
      required: true
    },
    getQuote: {
      type: Function,
      required: true
    }
  },
  updated() {
    console.log(this.bgColor);
    this.myStyle.backgroundColor = this.bgColor;
    this.textStyle.color = this.bgColor;
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Dancing+Script:wght@500&display=swap");

#quote-box {
  position: absolute;
  width: 600px;
  z-index: 15;
  top: 50%;
  left: 38%;
  margin: -100px 0 0 -100px;
  background-color: white;
  border-radius: 5px;
  box-shadow: 2px 2px 1px 1px #f0f8ff;
}

.buttons {
  margin: 5% 5%;
  display: flex;
  justify-content: space-between;
}

#tweet-quote {
  width: 30px;
  height: 32px;
  background-color: aqua;
  border: #f0f8ff;
}

#new-quote {
  border: #f0f8ff;
}

#quotation {
  font-size: 2em;
  margin-left: 0.8em;
  margin-right: 0.4em;
}

#text {
  font-family: "Dancing Script", cursive;
  font-size: 2rem;
  text-align: center;
}

#author {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-size: 1.2rem;
  margin-right: 10%;
}

.quote-author {
  align-items: right;
  text-align: right;
}

.quote-text {
  margin: 2% 5%;
}
</style>
