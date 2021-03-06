<template>
  <div>
    <slot></slot>
  </div>
</template>
<script>
import Vue from 'vue';
import $ from 'jquery';
import 'slick-carousel';

export default {

  props: {
    options: {
      type: Object,
      default() {
        return {};
      },
    },
  },

  mounted() {
    this.create();
  },

  beforeDestroy() {
    $(this.$el).slick('unslick');
  },

  methods: {
    create() {
      const $slick = $(this.$el);

      $slick.on('afterChange', this.onAfterChange);
      $slick.on('beforeChange', this.onBeforeChange);
      $slick.on('breakpoint', this.onBreakpoint);
      $slick.on('destroy', this.onDestroy);
      $slick.on('edge', this.onEdge);
      $slick.on('init', this.onInit);
      $slick.on('reInit', this.onReInit);
      $slick.on('setPosition', this.onSetPosition);
      $slick.on('swipe', this.onSwipe);
      $slick.on('lazyLoaded', this.onLazyLoaded);
      $slick.on('lazyLoadError', this.onLazyLoadError);

      $slick.slick(this.options);
    },

    reSlick() {
      $(this.$el).slick('unslick');
      this.create();
    },

    next() {
      $(this.$el).slick('slickNext');
    },

    prev() {
      $(this.$el).slick('slickPrev');
    },

    pause() {
      $(this.$el).slick('slickPause');
    },

    play() {
      $(this.$el).slick('slickPlay');
    },

    goTo(index, dontAnimate) {
      $(this.$el).slick('slickGoTo', index, dontAnimate);
    },

    currentSlide() {
      $(this.$el).slick('slickCurrentSlide');
    },

    add(element, index, addBefore) {
      $(this.$el).slick('slickAdd', element, index, addBefore);
    },

    remove(index, removeBefore) {
      $(this.$el).slick('slickRemove', index, removeBefore);
    },

    filter(filter) {
      $(this.$el).slick('slickFilter', filter);
    },

    unfilter() {
      $(this.$el).slick('slickUnfilter');
    },

    getOption(option) {
      $(this.$el).slick('slickGetOption', option);
    },

    setOption(option, value, refresh) {
      $(this.$el).slick('slickSetOption', option, value, refresh);
    },

    // Events
    onAfterChange(event, slick, currentSlide) {
      this.$emit('afterChange', event, slick, currentSlide);
    },

    onBeforeChange(event, slick, currentSlide, nextSlide) {
      this.$emit('beforeChange', event, slick, currentSlide, nextSlide);
    },

    onBreakpoint(event, slick, breakpoint) {
      this.$emit('breakpoint', event, slick, breakpoint);
    },

    onDestroy(event, slick) {
      this.$emit('destroy', event, slick);
    },

    onEdge(event, slick, direction) {
      this.$emit('edge', event, slick, direction);
    },

    onInit(event, slick) {
      this.$emit('init', event, slick);
    },

    onReInit(event, slick) {
      this.$emit('reInit', event, slick);
    },

    onSetPosition(event, slick) {
      this.$emit('setPosition', event, slick);
    },

    onSwipe(event, slick, direction) {
      this.$emit('swipe', event, slick, direction);
    },

    onLazyLoaded(event, slick, image, imageSource) {
      this.$emit('lazyLoaded', event, slick, image, imageSource);
    },

    onLazyLoadError(event, slick, image, imageSource) {
      this.$emit('lazyLoadError', event, slick, image, imageSource);
    },
  },

};
</script>
