<template>
    <div class="home">
        <h1>ToDoリスト</h1>
        <form>
            <input
                type="radio"
                name="todo"
                v-model="value"
                value="すべて"
                id="all"
            />
            <label for="all">すべて</label>
            <input
                type="radio"
                name="todo"
                v-model="value"
                value="作業中"
                id="work"
            />
            <label for="work">作業中</label>
            <input
                type="radio"
                name="todo"
                v-model="value"
                value="完了"
                id="completion"
            />
            <label for="completion">完了</label>
        </form>

        <table>
            <thead>
                <th>ID</th>
                <th>コメント</th>
                <th>状態</th>
            </thead>
            <tbody v-for="item in todoList" :key="item.id">
                <tr v-if="value === 'すべて'">
                    <td>{{ item.id }}</td>
                    <td>{{ item.comment }}</td>
                    <td>
                        <button @click="changeStatus(item.id)">
                            {{ item.status }}
                        </button>
                    </td>
                    <td>
                        <button @click="removeTask(item.id)">削除</button>
                    </td>
                </tr>

                <tr v-if="item.status === value">
                    <td>{{ item.id }}</td>
                    <td>{{ item.comment }}</td>
                    <td>
                        <button @click="changeStatus(item.id)">
                            {{ item.status }}
                        </button>
                    </td>
                    <td>
                        <button @click="removeTask(item.id)">削除</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <h2>新規タスクの追加</h2>
        <input type="text" v-model="task" />
        <button @click="addTask()">追加</button>
    </div>
</template>

<script>
export default {
    name: 'Home',
    data() {
        return {
            task: '',
            todoList: [],
            id: 0,
            status: '作業中',
            value: 'すべて',
        };
    },
    methods: {
        addTask() {
            for (let i = 0; i <= this.todoList.length; i++) {
                this.id = i;
            }

            this.todoList.push({
                id: this.id,
                comment: this.task,
                status: this.status,
            });

            this.task = '';
        },
        removeTask(num) {
            this.todoList.splice(num, 1);

            this.todoList.forEach((todo, index) => {
                todo.id = index;
            });
        },
        changeStatus(num) {
            if (this.todoList[num].status === '作業中') {
                this.todoList[num].status = '完了';
            } else {
                this.todoList[num].status = '作業中';
            }
        },
    },
};
</script>
