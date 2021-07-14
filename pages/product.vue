<template>
    <div>
        <NavBar />
        <EditProductModal :product="selectedProduct" />
        <DeleteProductModal :product="selectedProduct" @onDeleted="getAll" />

        <div class="container">
            <h1>
                Products
            </h1>
            
            <ProductEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-dark">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Description</th>
                        <th>Quantity</th>
                        <th>Price</th>
                        <th>Category</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="product in products" :key="product.id">
                        <td>{{product.name}}</td>
                        <td>{{product.description}}</td>
                        <td>{{product.quantity}}</td>
                        <td>{{product.price}}</td>
                        <td>{{product.category}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(product)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(product)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            products: [],
            selectedProduct: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/products')
            .then((res)=>{
                if (res.status==200) {
                    this.products = res.data
                }
            })
        },
        onEdit(selectedProduct) {
            this.selectedProduct = selectedProduct
            this.$bvModal.show('editProductModal')
        },
        onDelete(selectedProduct) {
            this.selectedProduct = selectedProduct
            this.$bvModal.show('deleteProductModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>