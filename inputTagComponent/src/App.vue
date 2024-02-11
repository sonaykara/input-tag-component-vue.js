<template>
 <div>
      <div class="tag-container">
        <span class="tag" v-for="(tag , index) in tags" :key="index">
            <span class="content-area">{{ tag }}</span>
            <span class="delete" @click="deleteButtonTag (index)"> X</span>
        </span>
      
        <input type="text" name="" id="" @keydown.enter="addedTag" @keydown.backspace="deleteTag">
        <div v-if="err" class="err">This tag has already been added</div>
      </div>
      
      
 </div>


</template>

<script>
  export default {

    data() {
      return {
        tags : [],
        err : false,
        
      }
    },

    methods : {
      addedTag (event) {
        let content = event.target.value
        let matchedTag = false
        if( content.length > 0){
          this.tags.forEach(tag => {
            if(tag.toLowerCase() === content.toLowerCase()) {
              matchedTag = true
            }
          })
          
          if(!matchedTag) {
            this.tags.push(content)
            content = ""
          } else {
            this.err = true
            setTimeout(() => {
                this.err = false
            }, 1000);
          }
        }
      },

      deleteTag (e) {
        if(e.target.value.length <= 0) {
          this.tags.splice(this.tags.length -1 , 1)
        }
      },

      deleteButtonTag (index) {
        this.tags.splice(index, 1)
      }
    }
    
  }
</script>

<style>
  .tag-container {
    padding: 15px;
    border: 1px solid #A81d04;
  }

  .tag {
    padding: 8px;
    color: #fff;
    background-color:#B5afad;
    cursor: default;
    font-size: 12px;
    margin-right: 7px;
    
  }

  .delete {
    font-size: 10;
    cursor: pointer;
  }

  input {
    height: 23px;
    width: 90px;
    outline: none;


  }

  .err {
    font-size: 10px;
    color:#A81d04;
    margin: 4px;
  }

</style>