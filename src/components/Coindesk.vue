<template>
  <div id="coindesk">
    <v-container fluid>
      <v-layout row wrap>
        <v-flex class="text-xs-center" justify-center xs12 sm12 md4 lg4 ma-2>
          <h1>Coin Desk Public Api Consumption Example</h1><br>
          <v-card v-for="coin in coindata">
            <v-img
              v-for="(img, index) in coinImages"
              v-if="img.currency === coin.currency"
              :key="'a' + index"
              :src="img.link"
              aspect-ratio="2.75"
            ></v-img>

            <v-card-title primary-title>
              <div>
                <h1 class="headline mb-0"> {{ coin.chartname }} / {{ coin.currency }}</h1>
                <h3>{{ coin.currencyVal[coin.currency].rate }}</h3>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>

import dollar from '@/assets/coindeskapi/img/dollar.jpg';
import pound from '@/assets/coindeskapi/img/pound.jpg';
import euro from '@/assets/coindeskapi/img/euro.jpg';

export default {
  name: 'coindesk',
  data: () => ({
      dialog: false,
      model: null,
      github: 'https://github.com/ThomasNaylor/coindeskAPIuse',
      coindata: [],
      coinImages: [
        { currency: 'USD', link: dollar },
        { currency: 'GBP', link: pound },
        { currency: 'EUR', link: euro }
      ]
    }),

    watch: {
      dialog (val) {
        val || this.close();
      }
    },

    created () {
      this.getCoinData();
    },

    methods: {
      close () {
        this.dialog = false;
      },

      getCoinData() {
        this.axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
        .then(response => {
          for(let coin in response.data.bpi) {
            this.coindata.push({
              chartname: response.data.chartName,
              currency: coin,
              currencyVal: response.data.bpi,
              timestamp: response.data.time
            });
          }
          return this.coindata;
        });
      }
  }
}
</script>

<style>

</style>
