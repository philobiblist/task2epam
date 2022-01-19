<template>
    <div>
        <app-stock v-for="stock in stocks" :stock="stock" :key="stock.id"></ap