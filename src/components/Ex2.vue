<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                newItem: ''
            }
        },
            methods: {
                addItem() {
                const trimmed = this.newItem.trim()
                if (trimmed) {
                    this.items.push(trimmed)
                    this.newItem = ''
                }
                },
                deleteItem(index) {
                this.items.splice(index, 1)
                }
            }

            
        }
    
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
     <ul>  
        <li v-for =  "(item,index) in items" :key='index' >{{ item }}
            <button @click = deleteItem(index)>Delete!</button>
        </li>
     </ul>

    <input 
        type="text" 
        placeholder="Candy"
        id='text'
        v-model="newItem"
        @keyup.enter = "addItem" >
        <button @click = "addItem">Add!</button>
    </input>
   
</template>
