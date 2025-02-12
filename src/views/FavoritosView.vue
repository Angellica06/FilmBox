<script setup>
</script>

<template>
    <main class="favorite">
        <section class="container text-center">
            <div class="content">
                <p class="">Sua lista de favoritos está vazia. Descubra novos filmes e séries agora!</p>
                <RouterLink class="btn" to="/">Explorar 🎬</RouterLink>
            </div>
        </section>
    </main>
</template>

<style scoped>
.favorite {
    padding-top: 4.8rem;
    min-height: 100vh;
    margin-top: 1.8rem;
}

.container {
    padding: 1rem;
    color: #fff718;
}

.content p {
    font-size: 1.2rem;
}

.btn {
    color: #1e1e1e;
    border: 0;
    background-color: #fff718;
    font-size: 1rem;
    font-weight: 600;
    transition: all .3s ease;
}

.btn:hover {
    transform: scale(1.04);
}
</style>