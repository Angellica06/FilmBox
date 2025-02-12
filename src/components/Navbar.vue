<template>
    <nav class="navbar shadow navbar-expand-lg fixed-top navbar-light bg-black">
        <div class="container">
            <div class="logo d-flex justify-content-center align-content-center mx-4 pt-1">
                <h1><RouterLink class="text-decoration-none logo" to="/">FilmBox</RouterLink></h1>
            </div>

            <button class="navbar-toggler" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasNavbar"
                aria-controls="offcanvasNavbar" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasNavbar"
                aria-labelledby="offcanvasNavbarLabel">
                <div class="offcanvas-header">
                    <button type="button" class="btn-close text-reset text-light" data-bs-dismiss="offcanvas"
                        aria-label="Close"></button>
                </div>
                <div class="offcanvas-body">
                    <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
                        <li class="nav-item overflow-hidden">
                            <RouterLink class="nav-link" to="/">Início</RouterLink>
                        </li>
                        <li class="nav-item overflow-hidden">
                            <RouterLink class="nav-link" to="/filmes">Filmes</RouterLink>

                        </li>
                        <li class="nav-item overflow-hidden">
                            <RouterLink class="nav-link" to="/series">Series</RouterLink>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </nav>
</template>

<style scoped>
.logo {
    background: -webkit-linear-gradient(#f2f2f2, #4c4c4c);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.navbar-toggler {
    border-color: #fff;
}

.navbar-toggler-icon {
    filter: brightness(0) invert(1);
}

.nav-link {
    color: #fff;
    font-size: 1rem;
    font-weight: 600;
}

.nav-link:hover {
    color: #fff718;
    transform: scale(1.01);
}

.nav-link:focus, .nav-link:active {
    color: #fff718 !important;
    outline: none;
}

.offcanvas-body,
.offcanvas-header {
    background-color: #000;
}

.offcanvas-header .btn-close {
    background-color: #fff718;
}
</style>