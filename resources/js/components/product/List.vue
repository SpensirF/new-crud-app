<template>
    <div class="row">
        <div class="col-12 mb-2 text-end">
            <router-link :to='{name:"productAdd"}' class="btn btn-primary">Create</router-link>
        </div>
        <div class="col-12">
            <div class="card">
                <div class="card-header">
                    <h4>Product</h4>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <thead>
                                <tr>
                                    <th>UUID</th>
                                    <th>Name</th>
                                    <th>Description</th>
                                    <th>Code</th>
                                    <th>Status</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody v-if="products.length > 0">
                                <tr v-for="(product,key) in products" :key="key">
                                    <td>{{ product.uuid }}</td>
                                    <td>{{ product.name }}</td>
                                    <td>{{ product.description }}</td>
                                    <td>{{ product.code }}</td>
                                    <td>{{ product.status }}</td>
                                    <td>
                                        <router-link :to='{ name:"productEdit" , params:{ id:product.id } }' class="btn btn-success">Edit</router-link>
                                        <button type="button" @click="deleteProduct(product.id)" class="btn btn-danger">Delete</button>
                                    </td>
                                </tr>
                            </tbody>
                            <tbody v-else>
                                <tr>
                                    <td colspan="4" align="center">No Products Found.</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    name:"products",
    data(){
        return{
            products:[]
        }
    },
    mounted(){
        this.getProducts()
    },
    methods:{
        async getProducts(){
            await this.axios.get('/api/product').then(response=>{
                this.products = response.data
            }).catch(error=>{
                console.log(error)
                this.products = []
            })
        },
        deleteProduct(id){
            if(confirm("Are you sure to delete this product ?")){
                this.axios.delete('/api/product/'+id).then(response=>{
                    this.getProducts()
                }).catch(error=>{
                    console.log(error)
                })
            }
        }
    }
}
</script>