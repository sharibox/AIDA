<template lang="html">
  <div class="elevation-1">
    <v-card class="panel">

      <v-toolbar
        id="toolbar"
        dense
      >
        <v-toolbar-title class="toolBarTitle">
          Channels
        </v-toolbar-title>
        <!-- <v-spacer/>
        <v-btn icon>
          <v-icon id="iconButton">
            add
          </v-icon>
        </v-btn> -->
      </v-toolbar>

      <v-list id="list" >
        <v-list-group
          v-for="(channel, index) in getChannels"
          :key="index"
          no-action
        >
          <v-list-tile
            class="list-hotfix"
            slot="activator"
            no-action
            @click.native="setActiveChannel(index)"
          >
            <v-list-tile-content>
              <v-list-tile-title
                class="faIcons">
                {{ channel.name ? channel.name : ('Channel ' + index) }}
              </v-list-tile-title>
            </v-list-tile-content>

          </v-list-tile>

          <!-- Layer Controls -->
          <div id="controls">
            <v-tabs
              left
              color="transparent"
            >
              <v-tab>
                <v-icon> visibility </v-icon>
              </v-tab>

              <v-tab>
                <v-icon> text_format </v-icon>
              </v-tab>

              <v-tab>
                <v-icon> delete </v-icon>
              </v-tab>

              <v-tabs-items id="tab-items">

                <!-- Opacity Slider -->
                <v-tab-item>
                  <div id="tab-item">
                    <v-layout
                      row
                      wrap>
                      <v-flex xs9>
                        <v-slider
                          v-model="channel.opacity"
                          step="0"
                          max="1"
                          @input="setChannelOpacity"
                        />
                      </v-flex>
                      <v-flex xs3>
                        <v-text-field
                          :value="(channel.opacity !== null) ? Math.round(channel.opacity*100) : 100"
                          suffix="%"
                          single-line
                          mask="###"
                          @change="setChannelOpacity"
                          @keyup.native.enter="setChannelOpacity"/>
                      </v-flex>
                    </v-layout>
                  </div>
                </v-tab-item>

                <!-- Rename List Item -->
                <v-tab-item>
                  <div id="tab-item">
                    <v-text-field
                      :value="channel.name ? channel.name : ('Channel ' + index)"
                      single-line
                      @change="setChannelName"
                      @keyup.native.enter="setChannelName"
                    />
                  </div>
                </v-tab-item>

                <!-- Delete List item -->
                <v-tab-item>
                  <div id="tab-item">
                    <v-btn
                      id="deleteButton"
                      small
                      color="error"
                      dark
                      flat
                      outline
                      @click="deleteChannel">
                      Delete
                    </v-btn>
                  </div>
                </v-tab-item>

              </v-tabs-items>
            </v-tabs>
          </div>

        </v-list-group>
      </v-list>

    </v-card>
  </div>
</template>

<script>
import { mapActions, mapState, mapGetters } from 'vuex'

export default {
  computed: {
    ...mapState({
      viewer: state => state.image.OSDviewer
    }),

    ...mapGetters({
      getChannels: 'image/getChannels'
    })
  },

  methods: {
    ...mapActions({
      setChannelOpacity: 'image/setChannelOpacity',
      setActiveChannel: 'image/setActiveChannel',
      setChannelName: 'image/setChannelName',
      deleteChannel: 'image/deleteChannel'
    })
  }
}
</script>

<style lang='css' scoped>
.panel {
  margin-top: 7px;
  background-color: #eeeeee;
}

.toolBarTitle {
  color: #424242;
}

#toolbar {
  background-color: #e0e0e0;
}

#iconButton {
  color: #616161;
}

#list {
  background-color: #eeeeee;
}

.list-hotfix {
  flex: 1 1 auto !important;
  overflow: hidden;
}

#controls {
  background-color: #f5f5f5;
  border-top: 1px solid #e0e0e0;
}

#tab-items {
  background-color: #fafafa;
}

#tab-item {
  height: 74px;
  padding: 0px 16px;
}

#deleteButton {
  margin: 18px 0 0;
}
</style>
