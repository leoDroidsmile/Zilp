<template>
  <div class="">
    <div class="row p-3">
      <div class="d-flex justify-content-center text-center">
        <h4>Balance : {{balanceWithDollar()}}</h4>
      </div>
    </div>
    <div class="row p-3">
      <div class="col-md-12 d-flex ">
        <div class="col-md-8 offset-2 input-group">
          <div class="input-group-prepend">
            <span class="input-group-text" id="inputGroupPrepend2">&#65504;</span>
          </div>
          <input type="text" class="form-control" v-model="deposit_amount" aria-describedby="inputGroupPrepend2">
        </div>
      </div>
    </div>

    <div class="iq-card-body">
        <ul class="nav nav-tabs" id="myTab-1" role="tablist">
          <li class="nav-item">
              <a class="nav-link active" id="home-tab" data-toggle="tab" href="#home" role="tab" aria-controls="home" aria-selected="true">Card</a>
          </li>
          <li class="nav-item">
              <a class="nav-link" id="profile-tab" data-toggle="tab" href="#profile" role="tab" aria-controls="profile" aria-selected="false">Paypal</a>
          </li>
          <li class="nav-item">
              <a class="nav-link" id="contact-tab" data-toggle="tab" href="#contact" role="tab" aria-controls="contact" aria-selected="false">Amazon</a>
          </li>
        </ul>
        <div class="tab-content" id="myTabContent-2">
          <div class="tab-pane fade show active pt-3" id="home" role="tabpanel" aria-labelledby="home-tab">
            <Stripe :depositAmount="deposit_amount"/>
          </div>
          <div class="tab-pane fade " id="profile" role="tabpanel" aria-labelledby="profile-tab">
            <div class="justify-content-center pt-3">
              <PayPal
                :amount="deposit_amount"
                currency="USD"
                :client="credentials"
                env="sandbox"
                payment-completed="paypalDepositCompleted()"
                payment-cancelled="paypalDepositCancelled()">
              </PayPal>
            </div>
          </div>
          <div class="tab-pane fade" id="contact" role="tabpanel" aria-labelledby="contact-tab">
            <div class="row justify-content-center pt-3">
              <div id="LoginWithAmazon"></div>
            </div>
            <Amazon :depositAmount="deposit_amount"/>
          </div>
        </div>
    </div>   
  </div>
</template>

<script>
import axios from 'axios'
import PayPal from 'vue-paypal-checkout'
import Stripe from './Stripe'
import Amazon from './Amazon'


// Paypal
// const PayPalButton = paypal.Buttons.driver("vue", window.Vue);

export default {
  name: 'Deposit',
  components: {
    PayPal, Stripe, Amazon
  },  

  data(){
    return {
      user: global.current_user,
      deposit_amount : '100.00',
      credentials: {
        sandbox: 'AfZpa0mZQUHVdstVt-WSbZLCHbawyaX_KDCnx2WgFA2wKL1FOX3nBmJYaf1vQMNOndv5WgEbE6Xd1Qef',
        production: 'EE2UQO-DG8e_KJrJrMNtv6oBatrDjF99n9l1leXc5wi29cpHlB6LpM3LR6_-3rLHfWWCrajZAEQgi0lO'
      },
    }
  },

  mounted: function () {
  },

  methods : {
    
    paypalDepositCompleted(response){
      console.log("Paypal desposit completed : ", response);
    },

    paypalDepositCancelled(response){
      console.log("Paypal desposit cancelled : ", response);
    }
  }
}
</script>
