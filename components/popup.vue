<template>
    <div class="popup_wrapper" ref="popup">
        <div class='popup'>
            <div class="popup__header">
                <span></span>
                <span class="close" @click="closePopup"></span>
            </div>
            <div class="popup__content">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'popup',
        data: () => ({

        }),
        methods: {
            closePopup() {
                this.$emit('closePopup')
            },
        },
        mounted() {
            let vm = this;
            document.addEventListener('click', function(item) {
                if (item.target === vm.$refs['popup']) {
                    vm.closePopup()
                }
            })
            window.addEventListener('keyup', function(event) {
                if (event.keyCode === 27) {
                    vm.closePopup()
                }
            });
        }

    }
</script>

<style lang="postcss">
    .close {
        box-sizing: border-box;
        position: relative;
        display: block;
        width: 22px;
        height: 22px;
        border: 2px solid;
        border-radius: 4px;
        cursor: pointer;

        &:after, &:before {
            content: "";
            display: block;
            box-sizing: border-box;
            position: absolute;
            width: 12px;
            height: 2px;
            background: currentColor;
            transform: rotate(45deg);
            border-radius: 5px;
            top: 8px;
            left: 3px;
        }
        &:after {
            transform: rotate(-45deg)
        }
    }
    .popup {
        padding: 16px;
        position: fixed;
        top: 50px;
        width: 400px;
        background: #ffffff;
        box-shadow: 0 0 17px 0 #e7e7e7;
        z-index: 10;

        &_wrapper {
            background: rgba(64,64,64, .4);
            display: flex;
            justify-content: center;
            align-items: center;
            position: fixed;
            right: 0;
            left: 0;
            top: 0;
            bottom: 0;
        }

        &__header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        &__content {
            display: flex;
            justify-content: center;
            align-items: center;
        }
    }
</style>