<template>
  <Test name="Why Attend Photo Location Test" :variations="variations">
    <template v-slot:loading>
      <div class="container mx-auto flex flex-wrap pt-4 pb-12" :style="{ minHeight: '515px' }"></div>
    </template>
    <template v-slot:default="{ variant }">
      <section class="bg-white border-b py-8">
        <div
          class="container mx-auto lg:flex lg:flex-wrap pt-4 pb-12"
          :style="variant.id === 'left' ? 'flex-direction: row' : 'flex-direction: row-reverse'"
        >
          <div class="lg:w-1/2">
            <img
              v-if="imageUrl.src"
              :src="imageUrl.src"
              :alt="imageUrl.alt || fields.title"
              :width="imageUrl.width"
              :height="imageUrl.height"
              class="p-10 lg:my-auto"
              loading="lazy"
            />
          </div>
          <div class="lg:w-1/2">
            <div class="p-10">
              <h2 class="w-full my-2 text-4xl font-bold leading-tight text-center text-gray-800">
                {{ fields.title }}
              </h2>
              <hr />
              <p class="text-gray-800 p-10 whitespace-pre-line">{{ fields.description }}</p>
            </div>
          </div>
        </div>
      </section>
    </template>
  </Test>
</template>

<script>
import { Test } from '@uniformdev/optimize-tracker-vue';
export default {
  name: 'why-attend',
  components: {
    Test,
  },
  props: {
    fields: {
      type: Object,
    },
  },
  computed: {
    variations() {
      return [{ id: 'left' }, { id: 'right' }];
    },
    imageUrl() {
      return {
        src: this.fields.image?.fields?.file?.url,
        alt: this.fields.image?.fields?.file?.fileName,
        height: this.fields.image?.fields?.file?.details?.image?.height,
        width: this.fields.image?.fields?.file?.details?.image?.width,
      };
    },
  },
};
</script>
