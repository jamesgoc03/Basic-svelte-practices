<script>
    import {v4} from 'uuid';
    import Toastify from 'toastify-js';
    import "toastify-js/src/toastify.css";

    let products = [];
    let editStatus = false;

    products = [...products,
        {
            id: v4(),
            name: "Lenovo thinkpad",
            description: "A laptop",
            imageUrl: null,
            category: "Laptops"
        },
        {
            id: v4(),
            name: "Mouse Raizer",
            description: "A peripheral",
            imageUrl: null,
            category: "Peripherals"
        }
    ]

    let product = {
        id: "",
        name: "",
        description: "",
        imageUrl: "",
        category: ""
    }

    const cleanProduct = () => {
        product = {
            id: "",
            name: "",
            description: "",
            imageUrl: "",
            category: ""
        }
    }

    const onSubmitHandler = (event) => {
        event.preventDefault();
        if(!editStatus) {
            addProduct()
        } else {
            updateProduct();
            editStatus = false;
        }

    };

    const addProduct = () => {
        const newProduct = {
            id: v4(),
            name: product.name,
            description: product.description,
            imageUrl: product.imageUrl,
            category: product.category
        }
        products = [...products, newProduct]
        new Toastify({
            destination: "https://github.com/apvarun/toastify-js",
            text: "Product " + product.name + " created successfully",
            duration: 3000,
            gravity: "bottom",
            position: "right",
            stopOnFocus: true,
            backgroundColor: "linear-gradient(to right, #28a745, #218838)"
        }).showToast();
        cleanProduct();
    }

    const updateProduct = () => {
        const updatedProduct = {
            id: product.id,
            name: product.name,
            description: product.description,
            imageUrl: product.imageUrl,
            category: product.category
        }
        products = products.map(product => product.id === updatedProduct.id ? updatedProduct : product);
        cleanProduct();
        new Toastify({
            destination: "https://github.com/apvarun/toastify-js",
            newWindow: true,
            text: "Product " + updatedProduct.name + " updated successfully",
            duration: 3000,
            gravity: "bottom",
            position: "right",
            stopOnFocus: true,
            backgroundColor: "linear-gradient(to right, #ffc107, #e0a800)",
        }).showToast();
    }

    const deleteProduct = (id) => {
        console.log(id);
        products = products.filter(product => product.id !== id);
        new Toastify({
            destination: "https://github.com/apvarun/toastify-js",
            newWindow: true,
            close: true,
            text: "Product deleted successfully",
            duration: 3000,
            gravity: "bottom",
            position: "right",
            stopOnFocus: true,
            backgroundColor: "linear-gradient(to right, #dc3545, #c82333)",
        }).showToast();
    }

    const editProduct = productToEdit => {
        product = productToEdit;
        editStatus = true;
    }

</script>

<main>

    <div class="container p-4">
        <div class="row">
            <div class="col-md-6">
                <h1>Products Registry</h1>
                <form onsubmit={onSubmitHandler}>
                    <div class="form-group">
                        <input
                                class="form-control"
                                bind:value={product.name}
                                type="text"
                                placeholder="Product name"
                                id="product-name">
                    </div>
                    <div class="form-group">
                        <textarea
                              class="form-control"
                              bind:value={product.description}
                              id="product-description"
                              rows="3"
                              placeholder="Product description">
                        </textarea>
                    </div>
                    <div class="form-group">
                        <input
                                class="form-control"
                                bind:value={product.imageUrl}
                                type="url"
                                id="product-image-url"
                                placeholder="https://www.yourImage.com">
                    </div>
                    <div class="form-group">
                        <select
                                class="form-control"
                                id="category" bind:value={product.category}
                        >
                            <option
                                    value="laptops">
                                Laptops
                            </option>
                            <option
                                    value="peripherals">
                                Peripherals
                            </option>
                            <option
                                    value="Servers">
                                Servers
                            </option>
                        </select>
                    </div>

                    <button class="btn btn-secondary" type="submit">
                        {#if !editStatus}
                            Save Product
                        {:else}
                            Update Product
                        {/if}
                    </button>
                </form>
            </div>
            <div class="col-md-6">
                <h1>Products</h1>
                {#each products as product}
                    <div class="card mt-2">
                        <div class="row">
                            <div class="col-md-4">
                                {#if product.imageUrl}
                                    <img alt="image of {product.name}" class="img-fluid p-2" src={product.imageUrl}/>
                                {:else}
                                    <img alt="image of {product.name}" class="img-fluid p-2" src="/src/assets/images/00-no-product.png"/>
                                {/if}
                            </div>
                            <div class="col-md-8">
                                <div class="car-body">
                                    <h5 class="pt-2">
                                        <strong>
                                            {product.name}
                                        </strong>
                                        <span>
                                        <small>
                                            <p>{product.category}</p>
                                        </small>
                                    </span>
                                    </h5>
                                    <p class="card-text">{product.description}</p>
                                    <button class="btn btn-danger" onclick={() => deleteProduct(product.id)}>
                                        Delete
                                    </button>
                                    <button class="btn btn-secondary" onclick={() => editProduct(product)}>
                                        Edit
                                    </button>
                                </div>

                            </div>
                        </div>
                    </div>
                {/each}
            </div>
        </div>
    </div>

</main>

<style>
</style>