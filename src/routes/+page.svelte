<script lang="ts">
	import StepItem from '$lib/components/StepItem.svelte';
	import type { Step } from '$lib/types';

	let steps = $state<Step[]>([
		{
			id: 'step-1',
			title: 'Prepare your workstation',
			body: 'Clean your work surface before handling the chocolate.'
		}
	]);

	let hasUntitledStep = $derived(steps.some((step) => step.title === ''));

	function addStep() {
		if (hasUntitledStep) return;

		steps.push({
			id: crypto.randomUUID().slice(0, 8),
			title: '',
			body: ''
		});
	}

	function deleteStep(id: string) {
		const step = steps.find((s) => s.id === id);
		if (!step) return;

		const label = step.title ? `“${step.title}”` : 'this step';
		if (!confirm(`Delete ${label}? This can’t be undone.`)) return;

		steps = steps.filter((s) => s.id !== id);
	}

	function moveStep(index: number, direction: -1 | 1) {
		const targetIndex = index + direction;
		if (targetIndex < 0 || targetIndex >= steps.length) return;

		const stepToMove = steps[index];
		steps[index] = steps[targetIndex];
		steps[targetIndex] = stepToMove;
	}
</script>

<svelte:head>
	<title>Attensi: Technical case - Frontend Developer</title>
</svelte:head>

<main class="mx-auto max-w-200 px-5 py-12">
	<h1 class="text-[2.25rem] leading-tight font-bold">Willy Wonka’s Chocolate Factory 🍫</h1>
	<p class="mt-3 leading-relaxed text-muted">Build your training scenario, one step at a time.</p>

	<ol class="mt-8 grid list-none gap-5 p-0">
		{#each steps as step, index (step.id)}
			<StepItem
				bind:step={steps[index]}
				stepNumber={index + 1}
				isFirst={index === 0}
				isLast={index === steps.length - 1}
				onMoveUp={() => moveStep(index, -1)}
				onMoveDown={() => moveStep(index, 1)}
				onDelete={() => deleteStep(step.id)}
			/>
		{/each}
	</ol>

	<button
		type="button"
		disabled={hasUntitledStep}
		aria-describedby={hasUntitledStep ? 'add-step-hint' : undefined}
		onclick={addStep}
		class="mt-5 cursor-pointer rounded-md bg-accent px-5 py-3 font-bold text-text hover:not-disabled:bg-accent-hover disabled:cursor-not-allowed disabled:opacity-50"
		>Add step</button
	>
	{#if hasUntitledStep}
		<p id="add-step-hint" class="pt-1 text-sm">Give each step a title before adding another.</p>
	{/if}
</main>
