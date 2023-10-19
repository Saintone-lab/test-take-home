<template>
    <div class="d-flex flex-column flex-shrink-0 p-3">
        <span class="fs-1 mb-5 mt-2 nav-brand">My Library</span>
        <ul class="nav nav-pills flex-column mb-auto fs-5">
            <li class="nav-header my-2">
                <span class="fs-4" style="font-weight: 600;">
                    Folder
                </span>
            </li>
            <li class="nav-item">
                <a href="#" class="nav-link active" aria-current="page">
                <i class="fi fi-rr-folder mr-2"></i>
                Camp Sinaraga
                </a>
            </li>
            <li>
                <a href="#" class="nav-link">
                <i class="fi fi-rr-add-folder"></i>
                Add Folder
                </a>
            </li>
        </ul>
    </div>
</template>

<script>

</script>

<style scoped>
    .nav-brand{
        text-align: center;
        font-weight: 800;
    }
    .nav-link{
        color: gray;
        border-radius: 5px;
    }
    .nav-link.active{
        color : rgb(106, 106, 244);
        background: rgb(229, 229, 255);
    }
</style>