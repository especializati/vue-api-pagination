<template>
    <div class="container">
        <h2 v-text="title"></h2>

        <div>
			<p><strong>Total registros:</strong> {{ products.total }}</p>
		</div>

		<table border="1" class="table table-dark table-hover">
			<tr>
				<th>id</th>
				<th>Name</th>
				<th>Description</th>
				<th width="200">Ações</th>
			</tr>
			<tr v-for="(product, index) in products.data" :key="index">
				<td>{{ product.id }}</td>
				<td>{{ product.name }}</td>
				<td>{{ product.description }}</td>
				<td>
                    <a href="#" class="btn btn-info">Editar</a>
					<a href="#" class="btn btn-danger">Deletar</a>
				</td>
			</tr>
		</table>

		<preloader-component
                        :preloader="preloader">
        </preloader-component>


		<pagination-component
                    :pagination="products"
                    @paginate="getProducts"
                    :offset="offset">
        </pagination-component>
    </div>
</template>

<script>
import PreloaderComponent from '../general/PreloaderComponent'
import PaginationComponent from '../general/PaginationComponent'

export default {
    data() {
        return {
            title: 'List Products', // title Page
            products: {
                total: 0,
                per_page: 10,
                from: 1,
                to: 0,
                current_page: 1,
                data: []
            },
            offset: 10, // Total Items por page (default)
            preloader: false, // Is Preloader is runing
        }
    },
    created () {
		this.getProducts()
	},
    methods: {
        getProducts () {
			this.preloader = true
			
			this.$http.get(`http://laravel55-webservice.local/api/v1/products?page=${this.products.current_page}`)
				.then(response => {
					console.log(response)
					this.products = response.data
				}, error => {
					console.log(error)
				})
				.finally(() => this.preloader = false)
		},
    },
	components: {
		PaginationComponent,
		PreloaderComponent,
	}
}

document.title = 'Lista de Produtos'

</script>

<style scoped>
</style>
