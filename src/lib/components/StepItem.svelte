<script lang="ts">
	import type { Step } from '$lib/types';
	import { ArrowUp, ArrowDown, Trash } from '@lucide/svelte';

	type Props = {
		step: Step;
		stepNumber: number;
		isFirst: boolean;
		isLast: boolean;
		onMoveUp: () => void;
		onMoveDown: () => void;
		onDelete: () => void;
	};

	let {
		step = $bindable(),
		stepNumber,
		isFirst,
		isLast,
		onMoveUp,
		onMoveDown,
		onDelete
	}: Props = $props();
</script>

<li
	class="grid grid-cols-[44px_minmax(0,1fr)] grid-rows-[auto_1fr] gap-x-2 rounded-xl border border-border bg-white p-4 text-text shadow-[0_2px_6px_#1c243305] sm:gap-x-5 sm:p-6"
>
	<h2
		class="col-start-1 row-start-1 grid size-11 place-items-center justify-self-center rounded-full bg-tint text-lg font-bold"
	>
		<span class="sr-only">Step </span>{stepNumber}
	</h2>

	<div class="col-start-2 row-span-2 row-start-1 min-w-0">
		<label class="sr-only" for="title-{step.id}">Step title</label>
		<div class="mb-3 flex items-center gap-2">
			<input
				id="title-{step.id}"
				type="text"
				placeholder="Step title"
				bind:value={step.title}
				class="h-11 w-full min-w-0 rounded-lg border border-border bg-white px-3 py-2 text-lg leading-relaxed font-bold placeholder:text-muted-2 focus-visible:outline-3 focus-visible:outline-offset-2 focus-visible:outline-accent-dark"
			/>

			<button
				type="button"
				aria-label="Delete step {stepNumber}"
				title="Delete step"
				onclick={onDelete}
				class="grid size-11 shrink-0 cursor-pointer place-items-center rounded-lg border-none bg-transparent text-muted hover:bg-danger-tint hover:text-danger focus-visible:outline-3 focus-visible:outline-offset-2 focus-visible:outline-accent-dark"
			>
				<Trash size={20} strokeWidth={1.6} aria-hidden="true" />
			</button>
		</div>

		<label class="sr-only" for="body-{step.id}">Step text</label>
		<textarea
			id="body-{step.id}"
			placeholder="What happens in this step?"
			bind:value={step.body}
			class="block min-h-28 w-full resize-y rounded-lg border border-border bg-white px-3 py-2 leading-relaxed font-normal placeholder:text-muted-2 focus-visible:outline-3 focus-visible:outline-offset-2 focus-visible:outline-accent-dark"
		></textarea>
	</div>

	<div
		class="col-start-1 row-start-2 mt-2 flex flex-col items-center justify-center gap-1 self-end"
	>
		<button
			type="button"
			disabled={isFirst}
			aria-label="Move step {stepNumber} up"
			title="Move up"
			onclick={onMoveUp}
			class="grid size-9 cursor-pointer place-items-center rounded-lg border-none bg-transparent text-muted hover:not-disabled:bg-tint hover:not-disabled:text-text focus-visible:outline-3 focus-visible:outline-offset-2 focus-visible:outline-accent-dark disabled:cursor-not-allowed disabled:opacity-30"
		>
			<ArrowUp size={20} strokeWidth={1.6} aria-hidden="true" />
		</button>

		<button
			type="button"
			disabled={isLast}
			aria-label="Move step {stepNumber} down"
			title="Move down"
			onclick={onMoveDown}
			class="grid size-9 cursor-pointer place-items-center rounded-lg border-none bg-transparent text-muted hover:not-disabled:bg-tint hover:not-disabled:text-text focus-visible:outline-3 focus-visible:outline-offset-2 focus-visible:outline-accent-dark disabled:cursor-not-allowed disabled:opacity-30"
		>
			<ArrowDown size={20} strokeWidth={1.6} aria-hidden="true" />
		</button>
	</div>
</li>
