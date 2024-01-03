<script setup>
    import { reactive } from 'vue';

    // const props = defineProps({
    //     modules: Array
    // });

    const data = reactive({
        modules: Array,
        perfil: {
            name: "Fulano de Tal",
            email: "fulanodetal@email.com",
            image: null
        }
    });

    if(!data.perfil.image)
        data.perfil.icon = 'person';

    data.modules = [
        {
            id:1,
            name: "exemplo 1",
            links: [
                {
                    id:1,
                    name: "exemplo 1",
                    selected: false,
                    url: "text"
                },
                {
                    id:2,
                    name: "exemplo 2",
                    selected: false,
                    url: "text"
                }
            ],
            class: '',
            selecticon: 'expand_more',
            icon: 'event_available'
        },
        {
            id:2,
            name: "exemplo 2",
            links: [
                {
                    id:1,
                    name: "exemplo 1",
                    selected: false,
                    url: "text"
                },
                {
                    id:2,
                    name: "exemplo 2",
                    selected: false,
                    url: "text"
                },
                {
                    id:3,
                    name: "exemplo 3",
                    selected: false,
                    url: "text"
                }
            ],
            class: '',
            selecticon: 'expand_more',
            icon: 'today',
        },
        {
            id:3,
            name: "exemplo 3",
            links: [],
            class: '',
            selecticon: 'expand_more',
            icon: 'fingerprint',
        }
    ];

    const toggleList = module => {
        module.class = module.class == 'open'
        ? ''
        : 'open';

        module.selecticon = module.selecticon == 'expand_more'
        ? 'expand_less'
        : 'expand_more'
    };

</script>

<template>
    <div class="side-bar">
        <div class="perfil">
            <div class="image" v-if="!data.perfil.image">
                <i class="material-icons">
                    {{ data.perfil.icon }}
                </i>
            </div>
            <div class="image" v-else>
                <img :src="data.perfil.image.src" :alt="data.perfil.image.name">
            </div>

            <div>
                <h4>
                    {{ data.perfil.name }}
                </h4>
                <h6>
                    {{ data.perfil.email }}
                </h6>
            </div>
        </div>

        <ul :key="m.id" v-for="m in data.modules" @click="toggleList(m)" :class="m.class">
            <span>
                <i class="material-icons">
                    {{ m.icon }}
                </i>
                <div>{{ m.name }} </div>
                <i class="material-icons">
                    {{ m.selecticon }}
                </i>
            </span>
            <li :key="l.id" v-for="l in m.links">
               <a :href="l.url"> {{ l.name }} </a>
            </li>
        </ul>
    </div>
</template>

<style>
.side-bar
{
    position: fixed;
    top: 10px;
    bottom: 0;
    margin: 4px;
    border-radius: 5px;
    background: #202124;
    color: white;
    width: 20%;
}

.side-bar > ul
{
    padding: 12px;
    margin: 4px;
}

.side-bar > ul:hover
{
    cursor: pointer;
    background: #303134;
}

.side-bar > ul.open
{
    background: #303134;
    overflow: hidden;
}

.side-bar > ul.open > li
{
    display: block;
    color: #3031349d;
}

.side-bar > ul.open > li > i
{
    color: rgba(255, 255, 255, 0.644);
}

.side-bar > ul.open > li:hover
{
    background: #1b1b1dab;
}

.side-bar > ul > span
{
    margin: 0;
    font-size: 20px;
    display: grid;
    grid-template-columns: 20% 60% 20%;
}

.side-bar > ul.open > span
{
    padding-bottom: 20px;
    border-bottom: solid 3px #1b1b1dab;
    display: grid;
    grid-template-columns: 20% 60% 20%;
}

.side-bar > ul > li
{
    font-size: 15px;
    list-style-type: none;
    display: none;
    padding: 10px;
    width: 100%;
}

.side-bar > ul > li > a
{
    text-decoration: none;
    color: rgba(255, 255, 255, 0.644);
}

.side-bar > .perfil
{
    display: grid;
    grid-template-columns: 40% 60%;
    align-items: center;
    background: #202124;
    border-radius: 4px;
    cursor: pointer;
}

.side-bar > .perfil > .image
{
    height: 100%;
    width: 100%;
    display: grid;
    align-items: center;
}

.side-bar > .perfil > .image > i
{
    padding: 20px;
    background: black;
}


</style>