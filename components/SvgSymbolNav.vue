<template>
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 180 180" class="w-full">
    <title lang="en">AIGA Midwest Design Week symbol</title>
    <g style="isolation: isolate">
      <g id="symbolNav">
        <rect
          x="90"
          width="90"
          height="90"
          class="symbolNavSquare fill-current text-red"
          style="mix-blend-mode: multiply"
        />
        <rect
          width="90"
          height="90"
          class="symbolNavSquare fill-current text-green"
          style="mix-blend-mode: multiply"
        />
        <rect
          x="90"
          y="90"
          width="90"
          height="90"
          class="symbolNavSquare fill-current text-teal"
          style="mix-blend-mode: multiply"
        />
        <rect
          ref="navButton"
          x="45"
          y="45"
          width="90"
          height="90"
          class="symbolNavSquare fill-current text-blue hover:text-blue-dark cursor-pointer transition-colors duration-300"
          style="mix-blend-mode: multiply"
          tabindex="0"
          role="button"
          aria-label="main menu button"
          aria-expanded="false"
          @click="toggleEvent"
          @keydown.enter="toggleEvent"
          @keydown.space="toggleEvent"
        />
        <transition
          enter-active-class="animated fadeIn faster"
          leave-active-class="animated fadeOut faster"
        >
          <g v-if="!navIsOpen" id="hamburger" key="h" class="pointer-events-none">
            <line
              x1="72.48"
              y1="98.73"
              x2="107.19"
              y2="98.73"
              stroke-linecap="round"
              stroke-miterlimit="10"
              stroke-width="4"
              class="stroke-current text-white"
            />
            <line
              x1="72.48"
              y1="89.9"
              x2="107.19"
              y2="89.9"
              stroke-linecap="round"
              stroke-miterlimit="10"
              stroke-width="4"
              class="stroke-current text-white"
            />
            <line
              x1="72.48"
              y1="81.07"
              x2="107.19"
              y2="81.07"
              stroke-linecap="round"
              stroke-miterlimit="10"
              stroke-width="4"
              class="stroke-current text-white"
            />
          </g>

          <g v-else id="hamburger-close" key="x" class="pointer-events-none">
            <line
              x1="77.57"
              y1="102.34"
              x2="102.1"
              y2="77.8"
              class="stroke-current text-white"
              stroke-linecap="round"
              stroke-miterlimit="10"
              stroke-width="4"
            />
            <line
              x1="77.57"
              y1="77.46"
              x2="102.1"
              y2="102"
              class="stroke-current text-white"
              stroke-linecap="round"
              stroke-miterlimit="10"
              stroke-width="4"
            />
          </g>
        </transition>
      </g>
    </g>
  </svg>
</template>

<script>
import { mapState } from 'vuex';

export default {
  name: 'SvgSymbol',

  computed: {
    ...mapState(['navIsOpen']),
  },

  mounted() {
    document.addEventListener('keydown', this.closeNav);
  },

  beforeDestroy() {
    document.removeEventListener('keydown', this.closeNav);
  },

  methods: {
    toggleEvent(e) {
      this.$emit('toggle-nav');
      e.target.setAttribute(
        'aria-expanded',
        e.target.getAttribute('aria-expanded') === 'false' ? 'true' : 'false'
      );
    },

    closeNav(e) {
      if (e.keyCode === 27) {
        this.$emit('close-nav');
        this.$refs.navButton.setAttribute('aria-expanded', 'false');
      }
    },
  },
};
</script>

<style lang="postcss" scoped></style>
