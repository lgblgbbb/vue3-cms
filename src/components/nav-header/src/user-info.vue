<template>
  <div class="user-info">
    <el-dropdown>
      <span class="el-dropdown-link">
        <el-avatar
          size="small"
          src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png"
        />
        <span class="info">{{ name }}</span>
      </span>
      <template #dropdown>
        <el-dropdown-menu>
          <el-dropdown-item @click="handleExit">退出登录</el-dropdown-item>
          <el-dropdown-item>用户信息</el-dropdown-item>
          <el-dropdown-item>系统管理</el-dropdown-item>
        </el-dropdown-menu>
      </template>
    </el-dropdown>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import { useStore } from 'vuex'
import localCache from '@/utils/cache'
import { useRouter } from 'vue-router'

export default defineComponent({
  setup() {
    const store = useStore()
    const name = computed(() => store.state.login.userInfo.name)

    const router = useRouter()
    const handleExit = () => {
      localCache.deleteCache('token')
      router.push('/main')
    }
    return {
      name,
      handleExit
    }
  }
})
</script>

<style scoped lang="less">
.el-dropdown-link {
  display: flex;
  align-items: center;
  .info {
    margin-left: 10px;
  }
}
</style>
