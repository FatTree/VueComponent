<template>
    <select v-model="selectedIndex">
        <option v-for="(item, index) in dataSource" :value="index">
            {{ item[dataName] }}
        </option>
    </select>    
</template>

<script>
export default {
    name: 'citySelector',
    props: [
        'oIndex',
        'dataSource',
        'dataName'
    ],
    computed: {
        selectedIndex: {
            get() {
                return this.oIndex;
            },
            set(val) {
                if (this.dataName == 'city') {
                    this.$emit('input', val);
                } else {
                    this.$emit('input2', val);
                }
                
            }
        }
    }
}
</script>
