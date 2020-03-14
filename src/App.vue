<template>
    <div id="app">
        <div id="nav">
            <router-link to="/">累计确诊</router-link> | 
            <router-link to="/info">疫情动态</router-link>
        </div>
        <router-view/>
    </div>
</template>

<style>
    #app{
        font-family: Arial, Helvetica, sans-serif;
        text-align: center;
        color: #2c3e50;
    }
    #nav{
        padding: 30px;
    }
    #nav a{
        font-weight: bold;
        color: #2c3e50;
    }

    #nav a.router-link-exact-active{
        color: #42b983;
    }
</style>