<template>
    <div>
        <transition-group tag="ul" name="users-list">
            <li
            v-for="user in users" :key="user"
            @click="removeUser(user)"
            >{{ user }}</li>
        </transition-group>
        
    </div>
    <div>
        <input 
        type="text"
        ref="enterredValue"
        >
        <button
        @click="addUser"
        >Add User</button>
    </div>

</template>

<script>

export default {
    data() {
        return {
            users: ['Naboth','Ongwenyi', 'Nyagoko'],
        }
    },
    methods: {
        removeUser(user) {
            this.users=this.users.filter(usr => usr !== user);
        },
        addUser() {
            const enteredUserName = this.$refs.enterredValue.value;
            this.users.unshift(enteredUserName);
        }
    }
}

</script>

<style scoped>
ul {
    list-style: none;
    margin: 1rem 0;
    padding: 0;
}
li {
    border: 1px solid #ccc;
    margin: 1rem;
    padding: 1rem;
    text-align: center;
}

.users-list-enter-from {
    opacity: 0;
    transform: translateX(-40px);
}
.users-list-enter-active {
    transition: all 1s ease-out;
}
.users-list-enter-to,
.users-list-leave-from{
    opacity: 1;
    transform: translateX(0);
}
.users-list-leave-active{
    transition: all 1s ease-in;
    position: absolute;
}

.users-list-leave-to{
    opacity: 1;
    transform: translateX(30px);
}

.users-list-move {
    transition: transform 0.8s ease;
}

</style>