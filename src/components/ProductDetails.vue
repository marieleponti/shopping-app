 <template>
        <ul>
            <li v-for="(size, i) in sizes"
            :key=i
            >
            {{ size }}
            </li>
        </ul>
 </template>
 

<script>
export default {
    data(){
        return {
            sizes: ["small", "medium", "large", "xl", "xxl"]
        }
    }
    
}
</script>


<style>

</style>

