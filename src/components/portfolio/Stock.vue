<template>
    <div>
        <div class="col-sm-6 col-md-4">
            <div class="panel panel-info">
                <div class="panel-heading">
                    <h3 class="panel-title">
                        {{ stock.name }}
                        <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
                    </h3>
                </div>
                <div class="panel-body">
                    <div class="pull-left">
                        <input
                                type="number"
                                class="form-control"
                                placeholder="Quantity"
                                v-model="quantity"
                                :class="{danger: insufficientQuantity}"
                        >
                    </div>
                    <div class="pull-right">
                        <button
                                class="btn btn-danger"
                                @click="sellStock"
                        >{{ insufficientQuantity ? 'Not enough' : 'Sell' }}
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <div class="alert alert-info col-sm-12 col-md-12" role="alert" v-if="purchased.flag">
            You have sold {{this.purchased.order.quantity}} units @{{this.purchased.order.stockPrice}} price successfully!
        </div>
    </div>
</template>

<style scoped>
    .danger {
        border: 1px solid red;
    }

    .alert-info {
        background-color: green !important;
        color: #fff;
        text-align: center;
        font-weight: bold;
    }
</style>

<script>
    import {mapActions} from 'vuex';

    export default {
        props: ['stock'],
        data() {
            return {
                quantity: 0,
                purchased: {
                    flag: false,
                    order: null
                }
            }
        },
        computed: {
          insufficientQuantity() {
              return this.quantity > this.stock.quantity;
          }
        },
        m