<template>
	<el-skeleton :loading="loading" :animated="animated" :class="['n8n-loading', `n8n-loading-${variant}`]">
		<template slot="template">
			<div v-if="variant === 'h1'">
				<div
						v-for="(item, index) in rows"
						:key="index"
						:class="{
						[$style.h1Last]: item === rows && rows > 1 && shrinkLast,
					}"
				>
					<el-skeleton-item
							:variant="variant"
					/>
				</div>
			</div>
			<div v-else-if="variant === 'p'">
				<div
						v-for="(item, index) in rows"
						:key="index"
						:class="{
						[$style.pLast]: item === rows && rows > 1 && shrinkLast,
					}">
					<el-skeleton-item
							:variant="variant"
					/>
				</div>
			</div>
			<div :class="$style.custom" v-else-if="variant === 'custom'">
				<el-skeleton-item
						:variant="variant"
				/>
			</div>
			<el-skeleton-item
					v-else
					:variant="variant"
			/>
		</template>
	</el-skeleton>
</template>

<script lang="ts">
import ElSkeleton from 'element-ui/lib/skeleton';
import ElSkeletonItem from 'element-ui/lib/skeleton-item';

import Vue from 'vue';

export default Vue.extend({
	name: 'n8n-loading',
	components: {
		ElSkeleton,
		ElSkeletonItem,
	},
	props: {
		animated: {
			type: Boolean,
			default: true,
		},
		loading: {
			type: Boolean,
			default: true,
		},
		rows: {
			type: Number,
			default: 1,
		},
		shrinkLast: {
			type: Boolean,
			default: true,
		},
		variant: {
			type: String,
			default: 'p',
			validator: (value: string): boolean => ['custom', 'p', 'text', 'h1', 'h3', 'text', 'caption', 'button', 'image', 'circle', 'rect'].includes(value),
		},
	},
});
</script>

<style lang="scss" module>
.h1Last {
  width: 40%;
}
.pLast {
  width: 61%;
}
.custom {
  width: 100%;
  height: 100%;
}
</style>

<style lang="scss">
.n8n-loading-custom .el-skeleton {
  &,
  .el-skeleton__item {
	width: 100%;
	height: 100%;
  }
}
</style>
