<template>
    <div>
        <b-modal id="editProductModal" title="Edit Product" ok-title="Save Product" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="product.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Description" label-for="description">
                <b-form-input id="description" v-model="product.description" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Quantity" label-for="quantity">
                <b-form-input id="quantity" v-model="product.quantity" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Price" label-for="price">
                <b-form-input id="price" v-model="product.price" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Manufactured Date" label-for="manufactured_on">
                <b-form-input id="manufactured_on" type="date" v-model="product.manufactured_on" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Category" label-for="category">
                <b-form-select v-model="product.category" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        product: {}
    },
    data() {
        return {
            options: [
                {value: 'food and drinks', text: 'Food and Drinks'},
                {value: 'beverage', text: 'Beverage'},
                {value: 'for cleaning', text: 'For Cleaning'},
                {value: 'personal use', text: 'Personal Use'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/products/' + this.product.id, this.product)
            .then((res)=>{
                if(res.status==202) {
                    alert('Edit successful!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>