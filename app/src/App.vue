<style>
  @import "~bootstrap/dist/css/bootstrap.min.css";
  @import "~font-awesome/css/font-awesome.css";
  * {
    margin: 0;
    padding: 0;
  }

  html,
  body { height: 100%; }
  body {
    align-items: center;
    background: url('./assets/img/bg.jpg');
    background-position: center;
    display: flex;
    font-family: Lato, Helvetica, sans-serif;
    justify-content: center;
    text-align: center;
    color: #eee;
  }

  body > div {
    width: 100%;
    height: 100%;
  } 
  .mask-custom {
    background-color: #337ab7;
    opacity: 0.2;
    min-height: 70px;
    margin-bottom: 20px;
  }
  .page-wrapper {
    padding-top: 70px;
  }
  .navbar-inverse {
    background-color: transparent;
    border-color: transparent;
  }

</style>

<template>
    <div>
      <div class="navbar-fixed-top mask-custom"> </div>
        <nav class="navbar navbar-inverse navbar-fixed-top navbar-custom">
        <nav-side></nav-side>
        </nav>
            <div class="page-wrapper">
                <keep-alive>
                    <router-view class="container-fluid" ></router-view>
                </keep-alive>
            </div>
        <Alert></Alert>
        <Popover></Popover>
  </div>
</template>

<script>
    import store from 'store';
    import NavSilde from './components/common/nav-side.vue';
    import { initTasks } from './api/task.js';
    import Alert from './components/base/alert.vue';
    import Popover from './components/base/popover.vue';

    export default {
        store,
        components: {
            'nav-side': NavSilde,
            Alert,
            Popover
        },
        async mounted() {
            await initTasks();
        },
        watch: {
            '$route': {
                handler(newValue, oldValue) {
                    // reset store
                    this.$store.dispatch('hidePopover');
                    this.$store.dispatch('hideAlert');
                }
            }
        }
    };
</script>
