<template>
  <div class="home">
    <div class="tool-bar">
      <v-menu>
        <template v-slot:activator="{ props }">
          <v-btn density="compact" rounded="0" variant="flat" color="primary" v-bind="props">
            文件
          </v-btn>
        </template>
        <v-list density="compact">
          <v-list-item v-for="(item, index) in items" :key="index" :value="index" @click="handleClick(item)">
            <v-list-item-title>{{ item.label }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-menu>
        <template v-slot:activator="{ props }">
          <v-btn density="compact" rounded="0" variant="flat" color="primary" v-bind="props">
            查看
          </v-btn>
        </template>
        <v-list>
          <v-list-item v-for="(item, index) in items" :key="index" :value="index">
            <v-list-item-title>{{ item.label }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-menu>
        <template v-slot:activator="{ props }">
          <v-btn density="compact" rounded="0" variant="flat" color="primary" v-bind="props">
            工具
          </v-btn>
        </template>
        <v-list>
          <v-list-item v-for="(item, index) in items" :key="index" :value="index">
            <v-list-item-title>{{ item.label }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </div>

    <v-dialog persistent v-model="createNewShow" transition="dialog-bottom-transition" width="40%" min-width="300px">
      <template v-slot:default="{ isActive }">
        <v-card>
          <v-toolbar color="primary" title="创建新连接"></v-toolbar>
          <v-card-text>
            <v-form ref="form">
              <v-text-field v-model="createNewForm.name" label="连接名" required></v-text-field>
              <v-text-field v-model="createNewForm.ip" placeholder="127.0.0.1" label="主机或ip地址" required></v-text-field>
              <v-text-field v-model="createNewForm.port" type="number" placeholder="3306" label="端口号"
                required></v-text-field>
              <v-text-field v-model="createNewForm.username" placeholder="admin" label="用户名" required></v-text-field>
              <v-text-field v-model="createNewForm.password" type="password" label="密码" required></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions class="justify-end">
            <v-btn variant="text" @click="createNewShow = false">关闭</v-btn>
            <v-btn @click="createNewShow = false">确定</v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

interface MenuItem {
  id: string,
  label: string
}

const createNewForm = ref({
  name: '',
  ip: '',
  port: '',
  username: '',
  password: ''
})

const createNewShow = ref(false)

const items: MenuItem[] = [
  {
    id: 'new',
    label: '创建新连接'
  },
  {
    id: 'export',
    label: '导出新连接'
  }
]

const handleClick = (v: MenuItem) => {
  switch (v.id) {
    case 'new':
      // 打开创建连接框
      createNewShow.value = true
      break;
    case 'export':
      break
  }
}
</script>

<style scoped>
.tool-bar {
  padding: 0;
  width: 1000%;
  background: #1867c0;
}
</style>
