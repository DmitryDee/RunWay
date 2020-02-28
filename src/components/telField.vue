<template>
  <div class="data-field"
        v-bind:class="{'data-field_active' : !showData}">
    <input type="tel" class="data-field__input"
            maxlength="18"
            placeholder="+7 (___)-__-__"
            v-bind:class="{'data-field__input_disabled' : showData, 'data-field__input_type_empty' : outputData}"
            v-bind:disabled="showData"
            v-bind:value="outputData" 
            v-on:input="inputValue"/> 
    <button class="data-field__btn"
            v-bind:class="{'data-field__btn_active' : !showData}"
            v-on:click="changeState"> 
      {{ state }}
    </button>
  </div>
</template>

<script>
let masked = IMask.createMask({
  mask: '+{7} (000) 000-00-00',
});

export default{
  props: {
    inputData: String
  },
  data(){
    return {
      outputData: this.inputData,
      showData: true,
      state: 'edit'
    }
  },
  created: function(){
  },
  methods:{
    inputValue($event){
      this.outputData = masked.resolve($event.target.value);
    },
    changeState(){
      this.state = (this.state == 'edit') ? 'save' : 'edit';
      this.showData = !this.showData;
      if(this.outputData !== this.inputData){
        this.$emit('dataChanged', this.outputData);
      }
    }
  },
  computed: {
  },
}

</script>

<style lang="scss">
  .data-field{
    &__input{

      &_disabled{
        border: none;
        padding: 0;
        background: none;
      }
    }
  }
</style>