<template>
  <div class="wrapper">
    <div class="wrapper__inner">
      <div class="wrapper__inner-content">
        <div class="header-logo">
          <div class="header-logo__container">
            <div class="header-logo__logo ibg">
              <img src="@/assets/logo.svg" alt="logo">
            </div>
          </div>
        </div>
        <main class="page">
          <section class="authorization authorization-main">
            <div class="authorization-main__container">
              <div class="authorization-main__wrapper">
                <div class="authorization-main__body">
                  <div class="authorization__title">Welcome back!</div>
                  <div class="authorization__subtitle">Enter your credentials to access your account</div>

                  <form action="#"  name="#" class="authorization__form form-authorization">
                  <!--  Email -->
                  <label for="authorization-email">
                    <Input
                        name="email"
                        autocomplete="off"
                        id="authorization-email"
                        placeholder="name@company.com"
                        label="Email"
                        :model-value="email"
                        :is-valide="isValide.email"
                        @update:modelValue="newValue => email = newValue"
                    />

                    <div v-show="!isValide.email" class="form-authorization__error-text">Invalid email format</div>
                  </label>

                  <!-- Password -->
                  <label for="authorization-password">
                    <Input
                        name="password"
                        autocomplete="off"
                        id="authorization-email"
                        placeholder="Input your password"
                        label="Password"
                        :model-value="password"
                        :is-valide="isValide.password"
                        @update:modelValue="newValue => password = newValue"
                    />

                    <div v-show="!isValide.password"  class="form-authorization__error-text">Password must be between 8 and 20 characters</div>
                  </label>

                    <a href="/forgot.html" class="form-authorization__link">Forgot password?</a>
                    <button
                        type="submit"
                        class="form-authorization__button"
                        :class="{'disabled': !isValide.email || !isValide.password}"
                        @click="submit"
                    >Sign in</button>
                  </form>
                </div>
                <div class="authorization__image">
                  <img src="@/assets/main-image.svg" alt="men">
                </div>

                <div class="authorization__dots authorization__dots_1">
                  <img src="@/assets/Dots.svg" alt="dots">
                </div>
                <div class="authorization__dots authorization__dots_2">
                  <img src="@/assets/Dots.svg" alt="dots">
                </div>
              </div>
            </div>
          </section>
        </main>
      </div>
    </div>
  </div>
</template>

<script>
import Input from "@/Controls/Input.vue";

export default {
  name: 'Auth',

  components: {
    Input,
  },

  data() {
    return {
      email: '',
      password: ''
    }
  },

  computed: {
    // Валидации почты и пароля
    isValide() {
      return {
        email: /^[^@]+@\w+(\.\w+)+\w$/.test(this.email),
        password: this.password.length >= 8
      }
    }
  },

  methods: {
    // Отправка данных
    submit() {
      const apiUrl = 'https://api.corecruiter.org/api/user/auth'
      const {email, password} = this
      const user = {
        email,
        password
      }

      fetch(apiUrl, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json;charset=utf-8'
        },
        body: JSON.stringify(user)
       }).then(async res => {
          res.status === 204 ? alert('OK') : alert('Mistake');
        });
    }
  }
}
</script>

<style scoped>
.disabled {
  pointer-events: none;
  opacity: 0.5;
}
</style>