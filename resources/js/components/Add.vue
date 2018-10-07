<template>
    <div class="modal" :class="openModal">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">Modal title</p>
            <button @click="dismissModal" class="delete" aria-label="close"></button>
            </header>
            <section class="modal-card-body">
                <div class="field">
                    <label class="label">Name</label>
                    <div class="control">
                        <input class="input" type="text" placeholder="Name" v-model="list.name">
                    </div>
                </div>
                <div class="field">
                    <label class="label">Phone</label>
                    <div class="control">
                        <input class="input" type="number" placeholder="Phone" v-model="list.phone">
                    </div>
                </div>
                <div class="field">
                    <label class="label">Email</label>
                    <div class="control">
                        <input class="input" type="email" placeholder="Email" v-model="list.email">
                    </div>
                </div>
            </section>
            <footer class="modal-card-foot">
            <button class="button is-success" @click="save">Save changes</button>
            <button class="button" @click="dismissModal">Cancel</button>
            </footer>
        </div>
    </div>
</template>

<script>
    export default {
        props: [
            'openModal'
        ],
        data() {
            return {
                list: {
                    name: '',
                    phone: '',
                    email:''
                }
            }
        },
        methods: {
            dismissModal() {
                this.$emit('closeModal');
            },
            save() {
                axios.post('/phonebook', this.$data.list)
                .then((response) => {
                    this.dismissModal();
                })
                .catch((error) => {
                    console.log(error);
                })
            }
        }
    }
</script>
