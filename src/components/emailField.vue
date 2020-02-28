<template>
  <div class="data-field"
        v-bind:class="{'data-field_active' : !showData}" >
    <span class="data-field__value"
          v-show="showData">
      {{ outputData }}
    </span>
    <input type="email" class="data-field__input"
            v-show="!showData"
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
  methods:{
    inputValue($event){
      this.outputData = $event.target.value;
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
  
</style>