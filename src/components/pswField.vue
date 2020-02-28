<template>
  <div class="data-field"
        v-bind:class="{'data-field_active' : !showData}">
    <input type="password" class="data-field__input"
            maxlength="16"
            placeholder="Password [********]"
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

export default{
  props: {
    inputData: String
  },
  data(){
    return {
      outputData: this.inputData,
      mask: 'Password [********]',
      showData: true,
      state: 'edit'
    }
  },
  methods:{
    inputValue($event){
      this.outputData = $event.target.value;;

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

<style lang="scss" scoped>
  
</style>