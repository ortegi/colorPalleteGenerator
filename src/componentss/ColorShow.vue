
<script setup>
    import {ref} from 'vue'
    const props = defineProps(['color', 'name'])

    const copyColor = () =>{
        navigator.clipboard.writeText(props.color)
        console.log(props.color)
        showMessage('color copied to clipBoard!')
    }

    const showMessage = (message, type = 'success') =>{
    Toastify({
        text: message,
        duration: 3000,
        destination: "https://github.com/apvarun/toastify-js",
        newWindow: true,
        close: true,
        gravity: "bottom", // `top` or `bottom`
        position: "right", // `left`, `center` or `right`
        stopOnFocus: true, // Prevents dismissing of toast on hover
        style: {
            background: type === "success" ? "green": "red"
        },
        onClick: function(){} // Callback after click
        }).showToast();

}

</script>


<template>
    <div class="card mt-3" style="width: 14rem; ">
        <div class="color" :style="{ backgroundColor: color}" > 
        </div>
        <div class="card-body">
            <p class="card-text text-center fw-bold fs-5"> {{ color }}</p>
            <p class="text-center fs-6 title"> {{ name }} </p>
            <button class="btn btn-outline-primary" @click="copyColor"> Copy!</button>
        </div>
      
    </div>
</template>

<style scoped>


.color{
    height: 200px;
    width: 12rem;
    margin: 10px auto;
    border-radius: 12px;
}

.title{
    height: 30px;
}
</style>