<template>
    <div class="row">
        <div class="col-12">
            <div class="card">
                <div class="card-header">
                    <h4>Update Product</h4>
                </div>
                <div class="card-body">
                    <form @submit.prevent="update">
                        <div class="row">
                            <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>UUID</label>
                                    <input type="text" class="form-control" v-model="product.uuid">
                                </div>
                            </div>
                            <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Name</label>
                                    <input type="text" class="form-control" v-model="product.name">
                                </div>
                            </div>
                            <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Description</label>
                                    <input type="text" class="form-control" v-model="product.description">
                                </div>
                            </div>
                            <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Code</label>
                                    <input type="text" class="form-control" v-model="product.code">
                                </div>
                            </div>
                            <div>
                                <label>Status:</label>
                                <b-form-select v-model="product.status" class="mb-3">
                                    <b-form-select-option value="active">Active</b-form-select-option>
                                    <b-form-select-option value="inactive">Inactive</b-form-select-option>
                                </b-form-select>
                            </div>
                            <div class="col-12 mb-2">
                                <button type="submit" class="btn btn-primary">Update</button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

export default{
    name:"update-product",
    data(){
        return{
            product:{
                uuid:"",
                name:"",
                description:"",
                code:"",
                status:"",
                _method:"patch"
            }
        }
    },
    mounted(){
        this.showProduct()
    },
    methods:{
        async showProduct(){
            await this.axios.get('/api/product/'+this.$route.params.id).then(response=>{
                const { uuid, name, description, code, status} = response.data
                this.product.uuid = uuid
                this.product.name = name
                this.product.description = description
                this.product.code = code
                this.product.status = status
            }).catch(error=>{
                console.log(error)
            })
        },
        async update(){ 
            await this.axios.post('/api/product/'+this.$route.params.id, this.product).then(response=>{
                this.$router.push({name:"productList"})
            }).catch(error=>{
                console.log(error)
            })
        }
    }
}
</script>