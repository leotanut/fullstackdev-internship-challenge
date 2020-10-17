<template>
  <div class="hello">
    <h1>List of drink</h1>
    <b-card-group deck>
      <b-card
        no-body
        v-for="item in list"
        :key="item.name"
        :img-src="item.image"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem"
        class="mb-2"
      >
        <b-card-body>
          <b-link to="/">
            <h4>{{ item.name }}</h4>
          </b-link>

          <p class="card-text">
            Price : {{ item.price }} <br />
            Status : {{ item.stock }}
          </p>

          <b-button v-on:click="adddrink(item)" href="#" variant="primary"
            >Select</b-button
          >
        </b-card-body>
      </b-card>
    </b-card-group>
    <div>
      <b-table striped hover :items="res" :fields="fields"></b-table>
    </div>

    <p v-for="index in res" :key="index.name">
      Coin inserted {{ coin }} Bath<button
        v-on:click="confirm(index)"
       id="show-btn" @click="showModal"
      >
        Confirm</button
      ><button v-on:click="cancel()">Cancel</button>
    </p>

    <div class="btn-group" role="group" aria-label="Basic example">
      <button type="button" class="btn btn-secondary" v-on:click="addcoin(10)">
        Add 10 bath
      </button>
      <button type="button" class="btn btn-secondary" v-on:click="addcoin(5)">
        Add 5 bath
      </button>
      <button type="button" class="btn btn-secondary" v-on:click="addcoin(2)">
        Add 2 bath
      </button>
      <button type="button" class="btn btn-secondary" v-on:click="addcoin(1)">
        Add 1 bath
      </button>
    </div>
    <div>

    <b-modal ref="my-modal" hide-footer title="You're welcome!!">
      <div class="d-block text-center">
        <p>{{ warning }}</p>
      <p>Change : {{ change }}</p>
      <li v-for="index in coinchange" :key="index.name">
        <p>Your coin change : {{ index }}</p>
      </li>
      <div v-for="(item, index) in allcoin" :key="(item, index)">
        <div v-if="item > 0">
          Coin {{ denominations[index] }} Bath x {{ item }}
        </div>
      </div>
      </div>
      <b-button class="mt-3" variant="outline-danger" block @click="hideModal">OK</b-button>
      
    </b-modal>
    </div>
  </div>
</template>
<script>
import axios from "axios";
// This imports <b-card> along with all the <b-card-*> sub-components as a plugin:
//import { CardPlugin } from "bootstrap-vue";

export default {
  name: "HelloWorld",
  data() {
    return {
      fields: ["name", "price"],
      coin: 0,
      change: 0,
      res: [],
      coinchange: [],
      denominations: [10, 5, 2, 1],
      allcoin: [0, 0, 0, 0],
      warning: "",

      list: "",
    };
  },
  mounted() {
    axios({
      method: "GET",
      url: "https://www.mocky.io/v2/5c77c5b330000051009d64c9",
    }).then(
      (result) => {
        this.list = result.data.data;

        for (let item in this.list) {
          if (this.list[item].in_stock === true) {
            this.list[item].stock = "Available";
          } else if (this.list[item].in_stock === false) {
            this.list[item].stock = "Sold out";
          }
        }
      },
      (error) => {
        console.error(error);
      }
    );
  },
  methods: {
    adddrink(i) {
      if (this.res.length == 0) {
        this.res.push(i);
      } else if (this.res.length == 1) {
        this.res.pop(i);
        this.res.push(i);
      }
    },
    addcoin(c) {
      if (this.res.length == 1) {
        this.coin += c;
        // this.allcoin.push(this.coin);
      }
    },
    confirm(i) {
      if (i.in_stock == true) {
        var index = 0;
        if (i.price == this.coin) {
          this.change = 0;
          this.warning = "Thank you";
          console.log(i.in_stock);
        } else if (i.price > this.coin) {
          this.warning = "Money isn't enough";
          this.change = this.coin;
          var usechange = this.change;
          while (usechange > 0) {
            if (usechange >= this.denominations[index]) {
              this.allcoin[index]++;
              usechange -= this.denominations[index];
            } else {
              index++;
            }
          }
          
        } else if (i.price < this.coin) {
           this.change = this.coin;
          this.change = this.coin - i.price;
          this.warning = "Thank you";
          var usechange2 = this.change;
          while (usechange2 > 0) {
            if (usechange2 >= this.denominations[index]) {
              this.allcoin[index]++;
              usechange2 -= this.denominations[index];
            } else {
              index++;
            }
          }
         
        }
      } else if (i.in_stock == false) {
        this.change = this.coin
        var index2 = 0;
        this.warning = "Goods is run out of stock";
            var usechange3 = this.change;
    while (usechange3 > 0) {
            if (usechange3 >= this.denominations[index2]) {
              this.allcoin[index2]++;
              usechange3 -= this.denominations[index2];
            } else {
              index2++;
            }
          }
      
    }
    },
    cancel() {
      (this.coin = 0),
        (this.change = 0),
        (this.coinchange = []),
        (this.warning = "");
    },     showModal() {
        this.$refs['my-modal'].show()
      },
      hideModal() {
        this.$refs['my-modal'].hide();
          this.allcoin= [0, 0, 0, 0];
           (this.coin = 0),
        (this.change = 0),
        (this.coinchange = []),
        (this.warning = "");
      },
    /*  toggleModal() {
        // We pass the ID of the button that we want to return focus to
        // when the modal has hidden
        this.$refs['my-modal'].toggle('#toggle-btn')
      }*/
  },
};
</script>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
