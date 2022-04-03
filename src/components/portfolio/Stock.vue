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
   