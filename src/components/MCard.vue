<template>
  <div
    :style="{ height: '100%' }"
    class="pa-2"
  >
    <v-card
      :color="theme.primary ? $tinycolor(theme.primary).darken().toString() : null"
      ripple
      hover
      height="100%"
      :href="site"
      :target="site ? '_blank' : ''"
      :style="{ overflow: 'hidden' }"
    >
      <v-img
        contain
        height="100%"
        :src="isImg ? logo : require('@/assets/sad_smiley.svg')"
        @error="renderLogo"
      >
        <v-layout
          fill-height
          align-end
          justify-center
        >
          <v-card-text :style="{ backgroundColor: 'rgba(0, 0, 0, .75)' }">
            <div
              :class="['font-weight-thin', 'white--text']"
              :style="{ fontSize: '2rem' }"
            >
              {{ name }}
            </div>
          </v-card-text>
        </v-layout>
      </v-img>
    </v-card>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  props: {
    name: {
      type: String,
      default: 'N/A',
    },
    logo: {
      type: String,
      // eslint-disable-next-line global-require
      default: require('@/assets/sad_smiley.svg'),
    },
    site: {
      type: String,
      required: false,
      default: null,
    },
  },
  data() {
    return {
      isImg: true,
      contextMenu: {
        isVisible: false,
        position: {
          x: 0,
          y: 0,
        },
      },
    };
  },
  computed: {
    ...mapState({
      theme(state) {
        return state.database.obj.theme || {};
      },
    }),
  },
  methods: {
    renderLogo() {
      this.isImg = false;
    },
    handleContextmenu(evt) {
      this.contextMenu.isVisible = true;
      this.contextMenu.position.x = evt.clientX;
      this.contextMenu.position.y = evt.clientY;
    },
  },
};
</script>
