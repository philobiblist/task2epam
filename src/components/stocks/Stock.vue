<template>
    <div>
        <div class="col-sm-6 col-md-4">
            <div class="panel panel-info">
                <div class="panel-heading">
                    <h3 class="panel-title">
                        {{ stock.name }}
                        <small>(Price: {{ stock.price }})</small>
                    </h3>
                </div>
                <div class="panel-body">
                    <div class="pull-left">
                        <input
                                type="number"
                                class="form-control"
                                placeholder="Quantity"
                                v-model="quantity"
                                :class="{danger: insufficientFunds}"
                        >
                    </div>
                    <div class="pull-right">
                        <button
                                class="btn btn-success"
                                @click="buyStock"
                        >{{ insufficientFunds ? 'Insufficient Funds' : 'Buy' }}
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <div class="alert alert-info col-sm-12 col-md-12" role="alert" v-if="purchased.flag">
            You have purchased {{this.purchased.order.quantity}} units @{{this.purchased.order.stockPrice}} price successfully!
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
            funds() {
                return this.$store.getters.funds;
            },
            insufficientFunds() {
                return this.quantity * this.stock.price > this.funds;
            }
        },
        methods: {
            buyStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };