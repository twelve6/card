# https://github.com/jessepollak/card
# Implementation for Electron-vue with Vuetify

### npm install package
```
npm install --save card
```

### !!ignore the following from the documentation, NO JQUERY REQUIRED AT ALL!!
```
var $ = require("jquery");
// The current card.js code does not explicitly require jQuery, but instead uses the global, so this line is needed.
window.jQuery = $;
var card = require("card");
```

### whitelist module in .electron-vue/webpack.rederer.config.js
```
let whiteListedModules = ['vue', 'vuetify', 'card']
```

## All the following I'm doing in a single componet file in renderer/components/AccountPage.vue

### import vue and card
```
import Vue from 'vue'
import * as Card from 'card'
```
### Instantiate Card in created, in nexttick or it will not render properly
```javascript
created () {
  Vue.nextTick(function () {
    // eslint-disable-next-line
    var card = new Card({
      form: '#creditcardform',
      container: '.card-wrapper'
    })
  })
}
```
### add the Veutify html
```html
<v-layout>
  <v-flex xs12 md6>
    <form action="" id="creditcardform">
      <v-text-field
        type="text"
        name="name"
        v-model="model.fullname"
        :rules="[() => !!model.fullname || 'Full Name is required']"
        label="Full Name*"
      ></v-text-field>

      <v-text-field
        type="tel"
        name="number"
        v-model="model.card"
        :rules="[() => !!model.card || 'Card Number is required']"
        label="Card Number*"
      ></v-text-field>

      <v-text-field
        type="tel"
        name="expiry"
        v-model="model.expiration"
        :rules="[() => !!model.expiration || 'Expiration is required']"
        label="MM /YY*"
      ></v-text-field>

      <v-text-field
        type="number"
        name="cvc"
        v-model="model.cvc"
        :rules="[() => !!model.cvc || 'CVC is required']"
        label="CVC*"
        @focus="invertedCard = true"
        @blur="invertedCard = false"
      ></v-text-field>
    </form>
  </v-flex>

  <v-flex xs12 md6 class="py-6">
    <div class="card-wrapper"></div>
  </v-flex>
</v-layout>
```
