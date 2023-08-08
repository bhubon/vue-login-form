<script setup>

</script>
<template>
    <div>
        <section class="flex h-screen w-full">
            <div class="w-1/2"
                style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
                <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">Kosmos!</h1>
            </div>
            <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200">
                {{ userLists }}
                {{ userInputs }}
                <h2 class="mb-5 text-xl">Login or register</h2>
                <div class="w-full max-w-xs">
                    <h2>Thanks for registering</h2>
                    <p class="text-center text-gray-500 text-xs">
                        &copy;2020 Acme Corp. All rights reserved.
                    </p>
                </div>
            </div>
        </section>
    </div>
</template>

<style lang="scss" scoped></style>