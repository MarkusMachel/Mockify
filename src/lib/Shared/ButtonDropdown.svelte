<script lang="ts">
    export let title: string;
</script>

<div>
    <button type="button">
        <slot {title}/>
    </button>
</div>>