<template>
  <seciton>
    <div class="card">
      <header class="card-header">
        <p class="card-header-title">
          Copy Github repository labels to another repository
        </p>
      </header>
      <div class="card-content">
        <div class="content">
          <b-notification type="is-success" closable="false">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce id
            fermentum quam. Proin sagittis, nibh id hendrerit imperdiet, elit
            sapien laoreet elit
          </b-notification>
          <form @submit.prevent="execute">
            <b-field>
              <template slot="label">
                <a href="https://github.com/settings/tokens" target="_blank">
                  Github Personal access token
                </a>
              </template>
              <b-input
                v-model="inputToken"
                icon="lock"
                type="password"
                password-reveal
                required
              ></b-input>
            </b-field>
            <b-field>
              <template slot="label">
                src repository (원본 저장소)
              </template>
              <b-input
                v-model="inputSrc"
                icon="link"
                required
                placeholder="ddarkr/easy-github-labels"
              ></b-input>
            </b-field>
            <b-field>
              <template slot="label">
                dest repository (목표 저장소)
              </template>
              <b-input
                v-model="inputDest"
                icon="link"
                required
                placeholder="ddarkr/easy-github-labels"
              ></b-input>
            </b-field>
            <hr />
            <p class="has-text-grey is-6">
              All API request is done at browser, and the token must have access
              to the repository.
            </p>
            <b-button type="is-primary">Execute!</b-button>
          </form>
        </div>
      </div>
    </div>
  </seciton>
</template>

<script>
import copyGithubLabels from 'copy-github-labels'

export default {
  data() {
    return {
      inputToken: '',
      inputSrc: '',
      inputDest: ''
    }
  },
  methods: {
    execute() {
      // 재사용 변수 초기화 후 시작.
      this.success = false
      this.error = ''

      // 라이브러리 로딩
      const cglInstance = copyGithubLabels()
      cglInstance.authenticate({
        token: this.inputToken
      })
      cglInstance.copy(this.inputSrc, this.inputDest, function(err, label) {
        // Handle errors
        if (err) {
          this.$buefy.notification.open({
            duration: 5000,
            message: `실패하였습니다! 자세한 오류 내용은 개발자 도구 Console을 참고해주세요.`,
            position: 'is-top-right',
            type: 'is-danger',
            hasIcon: true
          })
          // eslint-disable-next-line no-console
          console.log(err)
        }

        // 성공
        this.$buefy.notification.open({
          duration: 5000,
          message: `완료되었습니다.`,
          position: 'is-top-right',
          type: 'is-success',
          hasIcon: true
        })
      })
    }
  }
}
</script>
