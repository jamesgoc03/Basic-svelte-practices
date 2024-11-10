<script>
    import {createEventDispatcher} from "svelte";

    export let label;
    export let identifier;
    export let min;
    export let max;

    const dispatch = createEventDispatcher();

    function changeMin(event) {
        const newMin = parseInt(event.target.value);
        dispatch("update", {min: newMin, max});
    }

    function changeMax(event) {
        const newMax = parseInt(event.target.value);
        dispatch("update", {min, max: newMax,});
    }
</script>

<p>
    <label for={`${identifier}-min`}>{label} Min</label>
    <input type="range" min="0" max={50000} value={min} on:change={changeMin}>
    <span>{min}</span>
</p>
<p>
    <label for={`${identifier}-max`}>{label} Max</label>
    <input type="range" min="0" max={50000} value={max} on:change={changeMax}>
    <span>{max}</span>
</p>