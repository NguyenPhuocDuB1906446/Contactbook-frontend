<template>
    <div v-if="!submitted" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="createContact" />
        <p>{{ message }}</p>
    </div>
</template>

<script>

import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    

    data() {
        return {
            contact: {},
            message: "",
            submitted: false
            
        };
    },
    methods: {
        
        async addContact(data) {
            try {
                this.contact = await ContactService.create(data);
                this.submitted = true;
                this.message = "";
            } catch (error) {
                console.log(error);
            }
        },

        async createContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được tạo thành công.";
            } catch (error) {
                console.log(error);
            }
        },

    },

    newContact(){
        this.addContact(this.data);
        this.message = "";
    }


};
</script>