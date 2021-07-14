<template>
    <div>
        <b-modal id="deleteProductModal" title="Delete Product" ok-title="Delete Product" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this product? <br><br>
            Name: {{product.name}} <br>
            Description: {{product.description}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        product: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/products/' + this.product.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>