<template>
    <div class="row">
        <div class="col-12">
            <div class="card">
                <div class="card-header">
                    <h4>Add Product</h4>
                </div>
                <div class="card-body">
                    <form @submit.prevent="create">
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
                            <!-- <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Status</label>
                                    <input  class="form-check-input" type="checkbox"  v-model="product.status">
                                </div>
                            </div> -->
                            
                            <div>
                                <label>Status:</label>
                                <b-form-select v-model="product.status" class="mb-3">
                                    <b-form-select-option value="active">Active</b-form-select-option>
                                    <b-form-select-option value="inactive">Inactive</b-form-select-option>
                                </b-form-select>
                            </div>
                            <div class="col-12 mb-2">
                                <button type="submit" class="btn btn-primary">Save</button>
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
    name:"add-product",
    data(){
        return{
            product:{
                uuid:"",
                name:"",
                description:"",
                code:"",
                status:""
            }
        }
    },
    methods:{
        async create(){
            await this.axios.post('/api/product', this.product).then(response=>{
                this.$router.push({name:"productList"})
            }).catch(error=>{
                console.log(error)
            })
        }
    }
}
</script>