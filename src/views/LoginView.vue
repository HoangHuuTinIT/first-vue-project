<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

// Sử dụng ref để tạo các biến reactive, liên kết với các ô input trong form
// Dữ liệu người dùng nhập vào sẽ được tự động cập nhật vào các biến này
const email = ref('')
const password = ref('')
const rememberMe = ref(false)

// Hàm này sẽ được gọi khi người dùng nhấn nút "Đăng nhập"
function handleSubmit() {
  // Ngăn chặn hành vi mặc định của form (tải lại trang)
  // event.preventDefault(); // Vue đã xử lý việc này với @submit.prevent

  // Trong thực tế, đây là nơi bạn sẽ gửi dữ liệu đến server để xác thực
  console.log('Đang gửi dữ liệu đăng nhập:')
  console.log('Email:', email.value)
  console.log('Password:', password.value)
  console.log('Ghi nhớ đăng nhập:', rememberMe.value)

  // Sau khi xử lý, bạn có thể điều hướng người dùng đến trang khác
  // Bằng cách sử dụng vue-router
}
</script>

<template>
  <main class="login-page">
    <div class="login-form-container">
      <form @submit.prevent="handleSubmit">
        <h1>Đăng nhập</h1>
        <p class="subtitle">Chào mừng trở lại! Vui lòng nhập thông tin của bạn.</p>

        <div class="form-group">
          <label for="email">Địa chỉ Email</label>
          <input
            id="email"
            v-model="email"
            type="email"
            placeholder="nhapemail@gmail.com"
            required
          />
        </div>
        <div class="form-group">
          <label for="password">Mật khẩu</label>
          <input id="password" v-model="password" type="password" placeholder="••••••••" required />
        </div>

        <div class="form-options">
          <div class="remember-me">
            <input id="remember-me" v-model="rememberMe" type="checkbox" />
            <label for="remember-me">Ghi nhớ đăng nhập</label>
          </div>
          <RouterLink to="{name: 'forgot-password'}">Quên mật khẩu?</RouterLink>
        </div>

        <button type="submit" class="btn btn-primary">Đăng nhập</button>

        <div class="divider">
          <span>HOẶC</span>
        </div>

        <div class="social-login">
          <button type="button" class="btn btn-social">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
              <path
                fill="currentColor"
                d="M22.46 12.31c0-.81-.07-1.58-.2-2.31H12v4.36h5.84c-.25 1.41-.99 2.61-2.09 3.42v2.83h3.64c2.13-1.96 3.36-4.9 3.36-8.3z"
              />
              <path
                fill="currentColor"
                d="M12 23c3.23 0 5.93-1.07 7.91-2.91l-3.64-2.83c-1.07.72-2.43 1.15-4.27 1.15-3.28 0-6.06-2.21-7.05-5.18H1.26v2.91C3.25 20.3 7.27 23 12 23z"
              />
              <path
                fill="currentColor"
                d="M4.95 13.61c-.18-.54-.28-1.11-.28-1.7s.1-1.16.28-1.7V7.3H1.26c-.67 1.32-1.05 2.8-1.05 4.4s.38 3.08 1.05 4.4l3.69-2.9z"
              />
              <path
                fill="currentColor"
                d="M12 4.82c1.75 0 3.33.61 4.58 1.79l3.24-3.24C17.93 1.18 15.23 0 12 0 7.27 0 3.25 2.7 1.26 6.61l3.69 2.91c.99-2.97 3.77-5.18 7.05-5.18z"
              />
            </svg>
            <span>Đăng nhập với Google</span>
          </button>
        </div>

        <p class="register-link">
          Chưa có tài khoản?
          <RouterLink to="/register">Đăng ký ngay</RouterLink>
        </p>
      </form>
    </div>
  </main>
</template>

<style scoped>
/*
 * Bố cục và màu sắc được lấy cảm hứng từ các biến trong tệp `src/assets/base.css` của bạn
 * để đảm bảo tính nhất quán.
 */
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: var(--color-background-soft);
}

.login-form-container {
  width: 100%;
  max-width: 420px;
  padding: 2.5rem;
  background-color: var(--color-background);
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  border: 1px solid var(--color-border);
}

h1 {
  color: var(--color-heading);
  text-align: center;
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.subtitle {
  text-align: center;
  margin-bottom: 2rem;
  color: var(--color-text);
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: var(--color-text);
}

.form-group input {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1px solid var(--color-border);
  border-radius: 4px;
  background-color: var(--color-background-mute);
  color: var(--color-text);
  font-size: 1rem;
  transition:
    border-color 0.3s,
    box-shadow 0.3s;
}

.form-group input:focus {
  outline: none;
  border-color: hsla(160, 100%, 37%, 1);
  box-shadow: 0 0 0 2px hsla(160, 100%, 37%, 0.2);
}

.form-options {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
}

.remember-me {
  display: flex;
  align-items: center;
}

.remember-me input {
  margin-right: 0.5rem;
}

.forgot-password,
.register-link a {
  color: hsla(160, 100%, 37%, 1);
  text-decoration: none;
  transition: opacity 0.3s;
}

.forgot-password:hover,
.register-link a:hover {
  opacity: 0.8;
}

.btn {
  width: 100%;
  padding: 0.8rem 1rem;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition:
    background-color 0.3s,
    opacity 0.3s;
}

.btn-primary {
  background-color: hsla(160, 100%, 37%, 1);
  color: white;
}

.btn-primary:hover {
  opacity: 0.9;
}

.divider {
  text-align: center;
  margin: 1.5rem 0;
  color: var(--color-text);
  display: flex;
  align-items: center;
}

.divider::before,
.divider::after {
  content: '';
  flex-grow: 1;
  border-bottom: 1px solid var(--color-border);
}

.divider span {
  padding: 0 1rem;
}

.btn-social {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  background-color: var(--color-background-soft);
  color: var(--color-text);
  border: 1px solid var(--color-border);
}

.btn-social:hover {
  background-color: var(--color-background-mute);
}

.register-link {
  text-align: center;
  margin-top: 1.5rem;
}
</style>
