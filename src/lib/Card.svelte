<script>
    export let imageUrl = '';
    export let altText = '';
</script>

<style>
    .card {
        z-index: 100;
        position: absolute;
        top: 10px;
        right: 10px;
        background-color: white;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        overflow: hidden;
        width: 200px;
    }

    .card img {
        width: 100%;
        height: auto;
    }
</style>

<div class="card">
    <img src={imageUrl} alt={altText} />
    <h3>Card Title</h3>
    <p>Card content</p>
</div>