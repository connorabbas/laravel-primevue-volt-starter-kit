<script setup lang="ts">
import { useTemplateRef } from 'vue';
import Breadcrumb from '@/components/primevue/volt/Breadcrumb.vue';
import { ChevronRight } from 'lucide-vue-next';
import type { ExtendedMenuItem } from '@/types';

const componentProps = defineProps<{
    model: ExtendedMenuItem[]
}>();

type BreadcrumbType = InstanceType<typeof Breadcrumb>;
const childRef = useTemplateRef<BreadcrumbType>('child-ref');
defineExpose({
    childRef,
});
</script>

<template>
    <Breadcrumb
        ref="child-ref"
        :model="componentProps.model"
        pt:root:class="p-0 bg-transparent"
    >
        <template #item="{ item, props }">
            <InertiaLink
                v-if="item.route"
                :href="item.route"
                class="p-breadcrumb-item-link"
                custom
            >
                <i
                    v-if="item.icon"
                    :class="item.icon"
                    class="p-breadcrumb-item-icon"
                />
                <component
                    :is="item.lucideIcon"
                    v-else-if="item.lucideIcon"
                    class="p-breadcrumb-item-icon"
                />
                <span class="p-breadcrumb-item-label">{{ item.label }}</span>
            </InertiaLink>
            <a
                v-else
                :href="item.url"
                :target="item.target"
                v-bind="props.action"
            >
                <i
                    v-if="item.icon"
                    :class="item.icon"
                    class="p-breadcrumb-item-icon"
                />
                <component
                    :is="item.lucideIcon"
                    v-else-if="item.lucideIcon"
                    class="p-breadcrumb-item-icon"
                />
                <span class="p-breadcrumb-item-label">{{ item.label }}</span>
            </a>
        </template>
        <template #separator>
            <ChevronRight />
        </template>
    </Breadcrumb>
</template>
