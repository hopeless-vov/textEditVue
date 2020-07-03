<template>
    <div>


        <li   
        id="text" @mouseup="highlight" 
        class="region" 
        v-bind:style="{'color':color,'background-color': backgroundcolor, 'font-size': fontSize + 'px',}" 
          
        >
            <span v-bind:class="{done: todo.completed}">
                <input type="checkbox" 
                 v-on:change="todo.completed=!todo.completed" >
                <strong>{{index + 1}}</strong>
                {{todo.title}}  
            </span>
            <button 
                class="rm" 
                v-on:click="$emit('remove-todo', todo.id)"
            >&times;</button> 
        </li>
         
         

        <ul>
            <label v-for="color in colors"
             
            v-bind:key="color.id">
                
            <input type="radio" v-model="currentColor" :value="color">
            {{color}}
            </label>

            <input placeholder="color" type="text" v-model="color" />
            <input placeholder="backgroundcolor" type="text" v-model="backgroundcolor" />
            <input placeholder="size" type="number" v-model="fontSize" />
               
              
            
        </ul>
 
         
         
    </div>
</template>

<script>
 

export default {
    data() {
   return {
    color: '',
    font: '',
    backgroundcolor: '',
    fontSize:16,
    currentColor:'#ccc',
    colors: ["#ccc","#ff0000","#00ff00","#0000ff"],
    selectedRange:null
   }
        
    },
  computed:{
         
           
      },
   
  props:{
      todo: {
          type:Object,
          required:true
      },
      index: Number
  },
  methods: {
     getSelectedText() {
      if (window.getSelection) {
        let sel = window.getSelection()
        if (sel.getRangeAt && sel.rangeCount) {
          this.selectedRange = sel.getRangeAt(0);
        }
        return window.getSelection().toString()
      } else if (document.selection) {
        this.selectedRange = document.selection.createRange()
        return document.selection.createRange().text
      }
      return '' 
      
    },
    surroundSelection(color) {
      var span = document.createElement("span");
      span.className = 'highlight'
      span.style.fontWeight = "bold"
      span.style.color = color
      span.addEventListener("click", () => {
        console.log('click');
      });
      if (window.getSelection) {
        var sel = window.getSelection()
        if (sel.rangeCount) {
          var range = this.selectedRange.cloneRange()
          range.surroundContents(span)
          sel.removeAllRanges()
          sel.addRange(range)
        }
      }
    },
    highlight(){
    	let text = this.getSelectedText();
      if (this.selectedRange && text) {
          this.surroundSelection(this.currentColor)
        }
    }
  }
  
}
</script>
<style scoped>
    li {
        border: 1px solid #ccc;
        display:flex;
        justify-content: space-between;
        margin-bottom: 1rem;
        padding: .5rem 2rem;
        background-color:#fff;
         
        
    }
    .done {
        text-decoration: line-through;
    }
     
    .rm {
        background: red;
        color: #fff;
        border-radius: 50%;
        font-weight: bold;
      
    }
    input {
        margin-right: 1rem;
    }
      
</style>