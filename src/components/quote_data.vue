<template>
  <div>
    <div class="quotecontainer" v-if="quotecontainer">
      <!-- Quote -->
      <div class="quote-text">
        <img
          src="../assets/quote-left-solid.svg"
          alt=""
          class="quote-img"
          srcset=""
        />
        <span id="quote" :class="{ longquote: apidata.content.length > 100 }">{{
          apidata.content
        }}</span>
        <img
          src="../assets/quote-right-solid.svg"
          alt=""
          class="quote-img"
          srcset=""
        />
      </div>
      <!-- author -->
      <div class="quote-author">
        <span id="author">{{ apidata.author }}</span>
      </div>
      <!-- buttons -->
      <div class="button-container">
        <div id="twitter">
          <a :href="`https://twitter.com/intent/tweet?text=${apidata.content} By ${apidata.author}`" target="_blank">
            <img src="../assets/twitter-brands.svg" alt="" srcset="" />
          </a>
        </div>
        <a
          :href="`whatsapp://send?text=${apidata.content} -- ${apidata.author}`"
          target="_blank"
          class="twitter-button"
        >
          <img
            src="../assets/whatsapp-brands.svg"
            id="whatsapp_share"
            alt=""
            srcset=""
          />
        </a>
        <button id="new-quote" @click="callingapi">New Quote</button>
      </div>
    </div>
    <div class="loader" v-if="!quotecontainer"></div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      apidata: "",
      quotecontainer: false,
    };
  },
  created() {
    this.callingapi();
  },
  methods: {
    async callingapi() {
      await axios.get(`https://api.quotable.io/random`)
      .then((response) => {
        //   console.log(response);
        this.apidata = response.data;
        this.quotecontainer = true;
      });
    },
  },
};
</script>
<style>
#whatsapp_share {
  width: 60px;
  height: 60px;
}
#twitter {
  width: 60px;
  height: 60px;
}
/* #twitter:hover {
  background-color: #38a1f3;
} */
.quote-text .quote-img {
  height: 2.5rem;
}
.quotecontainer {
  width: auto;
  max-width: 900px;
  padding: 20px 40px;
  border-radius: 10px;
  background-color: rgba(255, 255, 255, 0.4);
  box-shadow: 0 10px 10px 10px rgba(0, 0, 0, 0.2);
}
.quote-text {
  font-size: 2.75rem;
}
.longquote {
  font-size: 2rem;
}
.fa-quote-left {
  font-size: 4rem;
}

.quote-author {
  margin-top: 15px;
  font-size: 2rem;
  font-weight: 400;
  font-style: italic;
}

.button-container {
  margin-top: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

button {
  cursor: pointer;
  font-size: 1.2rem;
  height: 2.5rem;
  border: none;
  border-radius: 10px;
  color: #fff;
  background: #333;
  outline: none;
  padding: 0.5rem 1.8rem;
  box-shadow: 0 0.3rem rgba(121, 121, 121, 0.65);
}

button:hover {
  filter: brightness(110%);
}

button:active {
  transform: translate(0, 0.3rem);
  box-shadow: 0 0.1rem rgba(255, 255, 255, 0.65);
}

.twitter-button:hover {
  color: #38a1f3;
}

.fa-twitter {
  font-size: 1.5rem;
}

/* Loader */
.loader {
  border: 16px solid #f3f3f3;
  border-top: 16px solid #333;
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
#whatsapp_share {
    display: none;
  }
/* Media Query: Tablet or Smaller */
@media screen and (max-width: 1000px) {
  .quotecontainer {
    margin: auto 10px;
  }

  .quote-text {
    font-size: 2.5rem;
  }
}
@media screen and (max-width: 767px) {
  #whatsapp_share {
    display: block;
  }
  #twitter {
    display: none;
  }
}
</style>
