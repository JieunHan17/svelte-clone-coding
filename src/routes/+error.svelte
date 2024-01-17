<script>
    import { page } from '$app/stores'
</script>

<h1>에러 페이지</h1>
<h2>{$page.status}: {$page.error && $page.error.message}</h2>