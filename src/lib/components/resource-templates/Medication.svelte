<script lang="ts">
  import { Badge} from 'sveltestrap';
  import type { Medication } from "fhir/r4";

  export let resource: Medication; // Define a prop to pass the data to the component
</script>

{#if resource.code}
  {#if resource.code.coding}
    <Badge color="primary">{resource.code.coding[0].system} : {resource.code.coding[0].code}</Badge>
    <br />
    {#if resource.code.coding[0].display}
      <strong>{resource.code.coding[0].display}</strong><br>
    {:else if resource.code.text}
      <strong>{resource.code.text}</strong><br>
    {/if}
  {:else if resource.code.text}
    <strong>{resource.code.text}</strong><br>
  {/if}
{/if}
{#if resource.ingredient}
  <table class="table table-bordered table-sm">
    <thead>
      <tr><th colspan="5">Composition</th></tr>
      <tr>
        <th scope="col">Ingredient</th>
        <th scope="col">Strength Numerator Qty</th>
        <th scope="col">Unit</th>
        <th scope="col">Strength Denominator Qty</th>
        <th scope="col">Strength Denominator Unit</th>
      </tr>
    </thead>
    {#each resource.ingredient as ingredient}
      <tr>
        <td>{ingredient.itemCodeableConcept?.coding?.[0].display}</td>
        <td>{ingredient.strength?.numerator?.value}</td>
        <td>{ingredient.strength?.numerator?.unit}</td>
        <td>{ingredient.strength?.denominator?.value}</td>
        <td>{ingredient.strength?.denominator?.unit}</td>
      </tr>
    {/each}
  </table>
{/if}
