<template>
    <div class="QuestionBox">
        <div class="jumbotron">
            <h5>{{ question.question }}</h5>
            <hr class="my-4">
            <p class="lead">List of answers</p>
            <button class="mx-2 btn btn-primary">Submit</button>
            <button class="mx-2 btn btn-success">Next</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "QuestionBox",
    props: {
        question: Object
    }
}
</script>

