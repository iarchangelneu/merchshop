<template>
    <div>
        <div class="course">
            <div class="course__left">
                <div>
                    <label for="name">Название товара</label>
                    <input type="text" id="name" name="name" placeholder="Введите название" ref="name" v-model="name">
                </div>
                <div>
                    <label for="name">Краткое описание</label>
                    <input type="text" id="name" name="name" placeholder="Введите краткое описание" v-model="shortDesc">
                </div>

                <div class="select">
                    <div class="mb-0">
                        <label for="select">Выберите категорию</label>
                        <select name="select" id="select" v-model="selectedCategory" ref="select">
                            <option v-for="(category, index) in categories" :key="index" :value="category.id">{{
                                category.name
                            }}</option>
                        </select>
                    </div>
                    <span v-if="selectedCategory !== null">
                        {{ getCategoryName(selectedCategory) }}
                        <img src="@/assets/img/del.svg" alt="" loading="lazy" @click="clearSelection">
                    </span>
                </div>

                <div class="discount">
                    <div>
                        <label for="name">Введите цену</label>
                        <input type="number" id="name" name="name" placeholder="Цена за товар" v-model="price">
                    </div>
                    <div>
                        <label for="name">Скидка, %</label>
                        <input type="number" id="name" name="name" placeholder="" v-model="discount" @input="limitValue">
                    </div>

                </div>
                <div>
                    <label for="name">Загрузка изображений (до 5)</label>
                    <div class="mb-0 fileupload" @dragover.prevent="highlightDropArea"
                        @dragleave.prevent="unhighlightDropArea" @drop.prevent="handleDrop" @click="openFileInput">
                        <span>{{ alert }}</span>
                        <small>Открыть</small>
                        <input type="file" ref="fileInput" style="display: none" accept="image/*" multiple
                            @change="handleFileInput" />
                    </div>


                    <div class="uploaded-images">
                        <div v-for="(image, index) in uploadedImages" :key="index" class="uploaded-image">
                            <img :src="image.url" alt="Uploaded Image" />
                        </div>
                    </div>
                </div>
            </div>

            <div class="course__right">
                <div>
                    <label for="tabs">Описание товара</label>
                    <ClientOnly>
                        <QuillEditor theme="bubble" toolbar="full" v-model:content="description" contentType="html" />
                    </ClientOnly>
                </div>
            </div>
        </div>

        <div class="text-center">
            <button ref="createProduct" @click="submitForm">Опубликовать товар</button>
        </div>

    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            selectedCategory: null,
            pathUrl: 'https://merchshop.kz',
            discount: 0,
            price: 0,
            name: '',
            modelname: 'фвывфы',
            shortDesc: '',
            description: '',
            alert: 'Перетащите файлы сюда или откройте вручную',
            uploadedImages: [],
            courseFeaturesText: '',
            categories: [
                { id: 1, name: "Стикеры" },
                { id: 2, name: "Одежда" },
                { id: 3, name: "Чехлы на телефон" },
                { id: 4, name: "Постеры" },
                { id: 5, name: "Для дома" },
                { id: 6, name: "Аксессуары" },
                { id: 7, name: "Для питомцев" },
                { id: 8, name: "Канцелярия" },
                { id: 9, name: "Для детей" },
                { id: 10, name: "Подарочные наборы" },
            ],
        }
    },

    methods: {
        async submitForm() {
            const csrf = this.getCSRFToken()
            if (this.name.length > 0) {
                this.$refs.name.style.borderColor = '#D2D2D2'

                if (this.selectedCategory != null) {
                    this.$refs.select.style.borderColor = '#D2D2D2'
                    const path = `${this.pathUrl}/api/seller/seller-lk/add-product/`
                    const formData = new FormData();

                    const filesToUpload = this.uploadedImages
                        .filter(item => item.file instanceof File)
                        .map(item => item.file);


                    formData.append('name', this.name);
                    formData.append('category', this.selectedCategory);
                    formData.append('price', this.price);
                    formData.append('discount', this.discount);
                    formData.append('description', this.description);
                    formData.append('key_features', this.courseFeaturesText);
                    formData.append('short_description', this.shortDesc);
                    filesToUpload.forEach(file => {
                        formData.append('add_image', file);
                    });
                    this.$refs.createProduct.disabled = true
                    this.$refs.createProduct.innerHTML = 'СОЗДАЕМ ЗАКАЗ'

                    try {
                        axios.defaults.headers.common['X-CSRFToken'] = csrf;
                        axios.defaults.headers.post['Content-Type'] = 'multipart/form-data';
                        const response = await axios.post(path, formData);
                        console.log('Форма успешно отправлена', response);
                        if (response.status == 201) {
                            this.$refs.createProduct.innerHTML = 'Заказ успешно создан!'
                        }
                    } catch (error) {
                        console.error('Ошибка при отправке формы', error);
                        this.$refs.createProduct.disabled = false
                        this.$refs.createProduct.innerHTML = 'Ошибка при создании заказа'
                    }
                }
                else {
                    this.$refs.select.style.borderColor = 'red'
                }
            }
            else {
                this.$refs.name.style.borderColor = 'red'
            }

        },
        handleKeyDown(event) {
            if (event.key === 'Backspace' && !this.courseFeaturesText) {
                event.preventDefault();
                return;

            }

            const lines = this.courseFeaturesText.split('\n');
            if (lines.length >= 6 && event.key === 'Enter') {
                event.preventDefault();
                this.$refs.featuresList.style.borderColor = 'red'
                return;
            }
        },
        getCategoryName(categoryId) {
            const category = this.categories.find((c) => c.id === categoryId);
            return category ? category.name : "";
        },
        clearSelection() {
            this.selectedCategory = null;
        },
        limitValue() {
            if (this.discount > 100) {
                this.discount = 100;
            }
        },
        highlightDropArea(event) {
            event.currentTarget.classList.add('highlight');
        },
        unhighlightDropArea(event) {
            event.currentTarget.classList.remove('highlight');
        },
        handleDrop(event) {
            event.preventDefault();
            this.unhighlightDropArea(event);

            const files = event.dataTransfer.files;
            this.processFiles(files);
        },
        handleFileInput() {
            const files = this.$refs.fileInput.files;
            this.processFiles(files);
        },
        processFiles(files) {
            const imageFiles = [];
            for (let i = 0; i < files.length; i++) {
                if (files[i].type.startsWith('image/')) {
                    imageFiles.push(files[i]);
                }
            }

            if (this.uploadedImages.length + imageFiles.length > 5) {
                this.alert = 'Можно загрузить не более 5х изображений'
                return;
            }

            imageFiles.forEach((file) => {
                const imageUrl = URL.createObjectURL(file);
                this.uploadedImages.push({ url: imageUrl, file });
            });

        },
        openFileInput() {
            this.$refs.fileInput.click();
        },
    }
}
</script>
<script setup>
import { QuillEditor } from '@vueup/vue-quill';
import '@vueup/vue-quill/dist/vue-quill.snow.css';
import '@vueup/vue-quill/dist/vue-quill.bubble.css';

useSeoMeta({
    title: 'Добавление курса | MerchShop',
    ogTitle: 'Добавление курса | MerchShop',
    description: 'Добавление курса | MerchShop',
    ogDescription: 'Добавление курса | MerchShop',
})


</script>
<style lang="scss" scoped>
.text-center {
    button {
        margin-top: 30px;
        padding: 10px 20px;
        border: 2px solid #828282;
        border-radius: 0;
        background: transparent;

        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
        text-transform: uppercase;
    }
}

.course {
    margin-top: 34px;
    display: flex;
    gap: 20px;
    width: 100%;

    @media (max-width: 1024px) {
        flex-direction: column;
        margin-top: 20px;
    }

    label,
    input {
        display: block;
    }

    label {
        margin-left: 10px;
        font-size: 16px;
        font-style: normal;
        font-weight: 500;
        line-height: 110%;
        font-family: var(--int);
        color: #000;
    }

    .uploaded-images {
        display: flex;
        flex-wrap: wrap;
        gap: 9px;
        margin-top: 20px;

        .uploaded-image {
            max-width: auto !important;
            width: auto !important;
        }

        img {
            width: 259px;
            height: 177px;

            @media (max-width: 1024px) {
                width: 165px;
                height: 110px;
            }
        }
    }

    input,
    select {
        background: transparent;
        border: 2px solid #D2D2D2;
        border-radius: 0;
        padding: 10px;
        width: 100%;

        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
    }

    .course__left {
        max-width: 527px;

        @media (max-width: 1024px) {
            max-width: 100%;
            width: 100%;
        }

        .highlight {
            border: 2px dashed green !important;
            cursor: pointer;
            /* Добавьте курсор-указатель, чтобы показать, что область можно нажать */
        }

        .fileupload {
            border-radius: 0;
            border: 2px solid #D2D2D2;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            cursor: pointer;


            span {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #3C3C3C;
            }

            small {
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                text-decoration-line: underline;
                font-family: var(--int);
                color: #000;
            }
        }

        width: 100%;

        div {
            margin-bottom: 20px;
            max-width: 527px;

            @media (max-width: 1024px) {
                max-width: 100%;
                width: 100%;
            }

            &:last-child {
                margin-bottom: 0;
            }
        }

        .discount {
            display: flex;
            gap: 10px;

            div {
                flex: 1;
            }
        }

        .select {
            display: flex;
            align-items: flex-end;
            flex-wrap: wrap;
            gap: 10px;

            @media (max-width: 1024px) {
                flex-direction: column;
                align-items: flex-start;
            }

            span {
                flex: 1;
                padding: 11px 10px;
                margin-top: 4px;
                border: 2px solid #D2D2D2;
                border-radius: 0;

                display: flex;
                align-items: flex-start;
                justify-content: space-between;
                gap: 10px;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;

                @media (max-width: 1024px) {}

                img {
                    cursor: pointer;
                }
            }
        }
    }

    .course__right {
        width: 100%;

        .custom-textarea {
            width: 100%;
            background: transparent;

        }

        .features-list {
            outline: none;
            white-space: pre-wrap;
            width: 100%;
        }

        textarea {
            width: 100%;
            border-radius: 0;
            border: 2px solid #D2D2D2;
            background: transparent;
            padding: 20px;
        }

        div {
            margin-bottom: 20px;

            &:last-child {
                margin-bottom: 0;
            }
        }
    }
}
</style>