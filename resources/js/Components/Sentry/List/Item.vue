<template>
    <div class="relative">
        <Link as="div" :href="event.route.show" class="cursor-pointer p-3 py-2 hover:bg-gray-50 dark:hover:bg-gray-800">
            <div class="flex flex-col md:flex-row md:items-center mb-1">
                <h3 class="text-blue-800 dark:text-blue-300 font-semibold pr-96">
                    {{ event.payload.type }}
                </h3>

                <span v-if="event.location" class="text-xs text-muted md:ml-3">
                    <strong>{{ location.filename }}</strong> in <strong>{{ location.function }}</strong>
                </span>
            </div>

            <pre class="text-xs break-all" v-html="event.payload.value"/>

            <div class="flex flex-col sm:flex-row sm:justify-between sm:items-center mt-3 text-xs text-muted">
                <div>
                    <span>{{ date }}</span>
                    <span class="mx-2">|</span>
                    <span><strong>logger: </strong>{{ event.logger }}</span>
                    <span class="mx-2">|</span>
                    <span><strong>env: </strong>{{ event.environment }}</span>
                </div>
                <Host :name="event.serverName" />
            </div>
        </Link>
    </div>
</template>

<script>
import Host from "@/Components/UI/Host";
import {Link} from '@inertiajs/inertia-vue3'
import JsonChip from "@/Components/UI/JsonChip";

export default {
    components: {
        JsonChip,
        Link, Host
    },
    props: {
        event: Object
    },
    computed: {
        date() {
            return this.event.date.fromNow()
        },
        location() {
            return this.event.location
        }
    }
}
</script>
