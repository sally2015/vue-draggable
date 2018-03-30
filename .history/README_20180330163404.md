<template>
	<Draggable v-model="cardList" :disabled="!dragSwitch"
	    @on-sort-ready="dragready" @on-sort-start="dragstart" @on-sort-end="dragend">
	    <template slot-scope="{item, index}">
	         <p>place your content here</p>              
	    </template>
	</Draggable>
</template>
<script>
import Draggable from './src/draggable';
export default{
	components: {
		Draggable
	}
}
</script>

用法：在vue项目中引入Draggale，components注册即可