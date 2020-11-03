<template>
    <div class="Header">
        <ul class="nav nav-tabs mb-5">
            <li class="nav-item">
                <a class="nav-link disabled">Vue Quiz App</a>
            </li>
            <li class="nav-item">
                <a class="nav-link disabled">{{ numCorrect }}/{{ numTotal }}</a>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Header",
    props: [
        "numCorrect",
        "numTotal"
    ]
}
</script>