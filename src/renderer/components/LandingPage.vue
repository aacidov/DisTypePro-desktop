<template>
<div>
  <init-page v-show='firstRun'></init-page>
  <div class="content-fluid" v-show='!firstRun'>
    <controlls></controlls>    
    <application></application>
    <settings v-show="settingsMenuData.active"></settings>
    <shortcuts v-show="shortcutsButtonData.active"></shortcuts>
    <show></show>
    
  </div>
  </div>
</template>

<script>
import { app } from "electron"
import swal from "sweetalert2"

import Application from "./LandingPage/Application"
import Settings from "./LandingPage/Settings"
import Controlls from "./LandingPage/Controlls"
import Shortcuts from "./LandingPage/Shortcuts"
import InitPage from "./LandingPage/InitPage"
import Show from "./LandingPage/Show"


export default {
  components: { Application, Controlls, Settings, Shortcuts, InitPage, Show },
  data() {
    return {
      settingsButtonData: Controlls.components.Settings.data(),
      shortcutsButtonData: Controlls.components.Shortcuts.data(),
      settingsMenuData: Settings.data(),
      firstRun: false
    }
  },
  watch: {
    firstRun(v) {
      this.$db.set("firstRun", v).write()
    }
  },

  methods: {
    open(link) {
      this.$electron.shell.openExternal(link)
    }
  },
  created() {
    this.firstRun = this.$db.get("firstRun").value()
  }
}
</script>

<style>
body,
#app {
  padding: 0;
  margin: 0;
  font-family: "sana";
}
.btn {
  overflow: hidden;
  word-wrap: normal;
  white-space: normal;
  margin: 1px;
  margin-bottom: 2px;
}
.success,
.btn-success,
.btn-success:active,
.btn:hover,
.btn-success:focus {
  background: white;
  color: black;
  border: none;
  margin-bottom: 1px;
  border-bottom: 1px solid #fbcc30;
}
</style>
