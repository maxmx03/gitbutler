<script lang="ts">
	import Tooltip from '@gitbutler/ui/Tooltip.svelte';
	import { type Snippet } from 'svelte';

	interface Props {
		isSelected: boolean;
		isNavCollapsed: boolean;
		tooltipLabel: string;
		alignItems?: 'center' | 'top';
		onmousedown: () => void;
		children: Snippet;
	}

	const {
		isSelected = false,
		isNavCollapsed = false,
		tooltipLabel,
		alignItems = 'center',
		onmousedown,
		children
	}: Props = $props();
</script>

<Tooltip text={isNavCollapsed ? tooltipLabel : ''} align="start">
	<button
		type="button"
		{onmousedown}
		class="domain-button text-14 text-semibold"
		class:selected={isSelected}
		class:align-center={alignItems === 'center'}
		class:align-top={alignItems === 'top'}
	>
		{@render children()}
	</button>
</Tooltip>

<style lang="postcss">
	.domain-button {
		display: flex;
		position: relative;
		padding: 10px;
		gap: 10px;
		border-radius: var(--radius-m);
		color: var(--clr-text-1);
		transition: background-color var(--transition-fast);
	}

	.domain-button::after {
		position: absolute;
		top: 0;
		left: -20px;
		width: 10px;
		height: 100%;
		transform: translateX(-100%);
		border-radius: var(--radius-s);
		background-color: var(--clr-theme-pop-element);
		content: '';

		transition: transform var(--transition-medium);
	}

	.domain-button.align-top {
		align-items: top;
	}

	.domain-button.align-center {
		align-items: center;
	}

	.domain-button:not(.selected):hover,
	.domain-button:not(.selected):focus {
		background-color: var(--clr-bg-1-muted);
	}

	.selected {
		background-color: var(--clr-bg-2);

		&::after {
			transform: translateX(0);
		}
	}
</style>
