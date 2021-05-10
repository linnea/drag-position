<template>
	<div class="container" ref="container"
		@touchstart="dragStart"
		@touchend="dragEnd"
		@touchmove="drag"
		@mousedown="dragStart"
		@mouseup="dragEnd"
		@mousemove="drag"
	>
	<div class="draggable" ref="item">
		<header
			class="drag-handle"
			ref="dragHandle"
		>
			Drag here
		</header>
		Draggable
	</div>
</div>
</template>

<script>

export default {
  name: 'Draggable',

  data () {
    return {
      dragItem: null,
      active: false,
      currentX: null,
      currentY: null,
      initialX: null,
      initialY: null,
      xOffset: 0,
      yOffset: 0
    }
  },

  mounted () {
    this.dragItem = this.$refs.item
  },

  methods: {
    setTranslate (xPos, yPos, el) {
      el.style.transform = 'translate3d(' + xPos + 'px, ' + yPos + 'px, 0)'
    },
    drag (e) {
      console.log('drag')
      if (this.active) {
        e.preventDefault()

        if (e.type === 'touchmove') {
          this.currentX = e.touches[0].clientX - this.initialX
          this.currentY = e.touches[0].clientY - this.initialY
        } else {
          this.currentX = e.clientX - this.initialX
          this.currentY = e.clientY - this.initialY
        }

        this.xOffset = this.currentX
        this.yOffset = this.currentY

        this.setTranslate(this.currentX, this.currentY, this.dragItem)
      }
    },
    dragEnd (e) {
      this.initialX = this.currentX
      this.initialY = this.currentY

      this.active = false
    },
    dragStart (e) {
      if (e.type === 'touchstart') {
        this.initialX = e.touches[0].clientX - this.xOffset
        this.initialY = e.touches[0].clientY - this.yOffset
      } else {
        this.initialX = e.clientX - this.xOffset
        this.initialY = e.clientY - this.yOffset
      }

      if (e.target === this.$refs.dragHandle) {
        this.active = true
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
	touch-action: none;
}

.draggable {
	width: 200px;
	height: 200px;
	border: 1px solid gray;
	border-radius: 4px;
	touch-action: none;
  	user-select: none;
}

.drag-handle {
	cursor: grab;
	background: #caa;
	border-bottom: 1px solid gray;
	padding: 8px;
}
</style>
