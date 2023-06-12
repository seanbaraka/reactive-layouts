<template>
    <section class="flex w-full relative">
        <aside class="bg-red-500 h-screen w-1/5 p-4">
        </aside>
        <main class="flex-1 flex">
            <div class="bg-green-700 h-screen w-1/3 p-4"></div>
            <slot />
        </main>
    </section>
</template>