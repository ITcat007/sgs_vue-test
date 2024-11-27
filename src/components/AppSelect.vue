<template>
    <label :for="name">
        <select :name="name" :id="name" v-model="localValue" @change="onChange">
            <option value="" class="option-default" disabled>{{ defaultOptionText }}</option>
            <option v-for="option in options" :key="option.id" :value="option.id">{{option.name}}</option>     
            {{option}}
        </select>
   </label>
</template>

<script>
  export default{
    props: {
        options: {
            type: Array
        },
        modelValue: {
          type: String,
          default: ''
        },
        defaultOptionText: {
            type: String        
        },
        name:{
            type: String,
            required: true          
        },
    },
      
    data() {
      return {
        localValue: this.modelValue !== null && this.modelValue !== undefined ? this.modelValue : ''
      }
    },

    methods: {
      onChange(event) {
        this.$emit('update:modelValue', event.target.value);
      }
    },
    
    watch: {
      modelValue(newValue) {
        this.localValue = newValue !== null && newValue !== undefined ? newValue : '';
      }
    }
  }
</script>

<style scoped>      
  select{
    width: 200px;
    height: 30px;
    background-color: #ffffff;
    border: 1px solid rgb(163, 163, 163);
    border-radius: 3px;
    margin-left: 10px;
  }
  
  .option-default{
      font-weight: 700;
  }
</style>