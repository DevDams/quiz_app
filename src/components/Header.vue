<template>
    <div class="header">
        <div class="container">
            <nav class="navbar mx-auto">
                <span class="navbar-brand mt-2 mb-0 h1 font-weight-bold">QUIZZYY 📝</span>
                <span class="navbar-text mt-2">
                    ✅ Correct Answer : {{ numCorrect }}/10
                </span>
            </nav>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: {
        numCorrect: Number,
    }
}
</script>

<style scoped>
.header {
    background: #025940;
    color: #F2D1C9;
    height: 80px;
}

.navbar {
    width: 80%;
}

.navbar-brand {
    font-size: 30px;
}


@media (max-width: 540px) {
    .navbar {
        width: 100%;
    }
}

@media (max-width: 432px) {
    .header {
        height: 130px;
    }
}
</style>
