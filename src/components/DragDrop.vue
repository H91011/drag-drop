<template>
  <div class="drag-drop">

      <div class="drag-area" ref="dragArea">

      <div class="drag-elem" ref="dragElem"> 
        <p ref="dragElemChild">drag elem </p> 
      </div>

      </div>
  </div>
</template>

<script>
export default {
  name: 'DragDrop',
  props: {},
  data(){
    return {
      mouseDown: false,
    }
  },

  mounted(){
    document.addEventListener("mousedown", (e)=>{
      if(e.target == this.$refs["dragElem"] || e.target == this.$refs["dragElemChild"] ){
        this.mouseDown = true
      }
    })

    document.addEventListener("mousemove", (e)=>{
      if(this.mouseDown){

        const {x,y, width, height } = this.$refs["dragArea"].getBoundingClientRect();

        const b2 = this.$refs["dragElem"].getBoundingClientRect();

        const widthHalf= b2.width/2
        const heightHalf = b2.height/2

        const dx = e.x - x 
        const dy = e.y - y 

        if(dx > widthHalf){
          this.$refs["dragElem"].style.left = (dx)- widthHalf+"px"
        } else {
          this.$refs["dragElem"].style.left = "1px"
        }

        if(dy > heightHalf){
          this.$refs["dragElem"].style.top = (dy)- heightHalf+"px"
        } else {
          this.$refs["dragElem"].style.top = "1px"
        }

        if(dx > width- b2.width){
          this.$refs["dragElem"].style.left = (width - b2.width-1)+"px"
        }

        if(dy > height- b2.height){
          this.$refs["dragElem"].style.top = (height - b2.height-1)+"px"
        }
      }
    })


    document.addEventListener("mouseup", ()=>{
      this.mouseDown = false
    })


  },

  methods: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.drag-elem{
  position: absolute;
}


.drag-drop{
  width: 100%;
  height: 100vh;
  background-color: aquamarine;
}

.drag-area{
  position: absolute;
  margin:5%;
  width: 90%;
  height: 75%;
  background-color: rgb(213, 201, 201);

}

.drag-elem{
  width: max-content;
  border: solid 2px green;
  background-color: rgb(0, 255, 221);
  border-radius: 25px;
}

.drag-elem p {
   margin: 5px;
}


</style>
