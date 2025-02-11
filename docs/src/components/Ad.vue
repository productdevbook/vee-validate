<template>
  <div v-if="!hasError" id="ad" :class="{ 'placement-home': placement === 'home-page' }"></div>
  <div v-else id="ad" class="error">
    <div class="p-4 flex flex-col">
      <span class="font-bold font-display">🙏 Enable Ads</span>
      <span class="mt-2"> Please enable ads on your browser for this website. </span>
      <span class="mt-1"> Ads are a funding source to this project. </span>

      <div class="mt-2 or-fund-it">
        <span class="mx-1 whitespace-nowrap">or consider</span>
      </div>

      <a
        target="_blank"
        rel="noopener"
        href="https://github.com/sponsors/logaretm"
        class="mt-2 bg-pink-600 py-1 px-2 text-white font-medium flex items-center justify-center font-display rounded group hover:bg-pink-700"
      >
        <svg
          class="stroke-current transform transition duration-200 group-hover:scale-110 w-5 h-5 mr-1"
          fill="none"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
          ></path>
        </svg>

        Sponsor
      </a>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';

defineProps<{
  placement?: 'content' | 'home-page';
}>();

const hasError = ref(false);

function loadScript() {
  const script = document.createElement('script');
  script.src = '//cdn.carbonads.com/carbon.js?serve=CE7DKKQ7&placement=vee-validatelogaretmcom';
  script.id = '_carbonads_js';

  const el = document.querySelector('#ad');
  el?.appendChild(script);
  script.onerror = error => {
    if (navigator.onLine) {
      hasError.value = true;
    }
  };
}

onMounted(loadScript);
</script>

<style lang="postcss">
#ad {
  @apply static text-gray-400 mt-4;
  z-index: 1;

  #carbonads {
    display: block;
    overflow: hidden;
    box-shadow: 0 1px 3px hsla(0, 0%, 0%, 0.05);
    border-radius: 4px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue',
      Helvetica, Arial, sans-serif;
    line-height: 1.5;
    max-width: 300px;
    font-size: 12px;
    background-color: #fff;
  }

  #carbonads a {
    text-decoration: none;
  }

  #carbonads span {
    position: relative;
    display: flex;
    overflow: hidden;
  }

  .carbon-img img {
    display: block;
    @apply mx-auto;
  }

  .carbon-text {
    @apply p-2 block float-left text-left;
    max-width: calc(100% - 130px - 1em);
    color: currentColor;
    padding-bottom: 20px;
  }

  .carbon-poweredby {
    @apply p-2 absolute bottom-0 block uppercase;
    left: 142px;
    bottom: 0;
    font-size: 10px;
    color: currentColor;
    font-weight: 500;
    line-height: 1;
    letter-spacing: 1px;
  }
}

@screen lg {
  #ad {
    @apply rounded-md ml-0;
    left: unset;
    float: unset;
    width: 160px;
    z-index: 19;
    background-color: #fff;
    font-size: 13px;
    #carbonads {
      padding-top: 15px;
      max-width: 100%;
    }

    #carbonads span {
      @apply flex-col;
    }

    .carbon-img {
      margin: 0;
    }

    #carbonads,
    .carbon-wrap {
      display: flex;
      flex-direction: column;
    }

    .carbon-text {
      margin-top: 10px;
      max-width: 100%;
    }

    .carbon-poweredby {
      position: static;
      margin-top: 10px;
    }

    &.placement-home {
      left: unset;
    }
  }
}

.dark {
  #ad {
    #carbonads {
      @apply bg-zinc-800;
    }

    &.error {
      @apply bg-zinc-800;
    }
  }
}

.or-fund-it {
  @apply text-zinc-500 flex items-center space-x-2;

  &::before,
  &::after {
    height: 1px;
    width: 100%;
    content: '';
    @apply flex-shrink bg-zinc-500;
  }
}
</style>
