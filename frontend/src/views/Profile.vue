<template>
  <div class="animated fadeIn">
      <b-row>
        <b-col sm="2">
          <div>
            <b-img center rounded="circle" blank width="175" height="175" blank-color="#777" alt="img" class="m-1" />
            <p class="text-center">Profile</p>
          </div>
          <div>
            <p class="text-center">Name : <strong>{{ profile.name }}</strong></p>
            <p class="text-center">LV 1 / SI : <strong>{{ profile.si }}</strong></p>
            <p class="text-center">Cherry : <strong>{{ tokens }}</strong></p>
            <p class="text-center">Questions : <strong>{{ questions.length }}</strong></p>
            <p class="text-center">Answers : <strong>{{ answers.length }}</strong></p>
            <p class="text-center">Likes : <strong>{{ likes.length }}</strong></p>
            <p class="text-center">Comments : <strong>{{ comments.length }}</strong></p>
          </div>
          <br/>
          <div class="text-center">
            <b-button variant="success" :to="{name: 'Cherry Transfer'}">Cherry Transfer</b-button>
          </div>
        </b-col>
        <b-col sm="10">
          <b-tabs>
            <b-tab title="알림" active>
              <b-list-group flush>
                <b-list-group-item>
                  <span class="text-success">blossommmm</span><span class="text-muted">님이 당신의 질문에 답하였습니다.</span> "제 보험 한번만 봐주세요.." <span class="text-warning">2 hours ago</span>
                </b-list-group-item>
                <b-list-group-item>
                  <span class="text-success">blossommmm</span><span class="text-muted">님이 당신의 질문에 답하였습니다.</span> "제 보험 한번만 봐주세요.." <span class="text-warning">2 hours ago</span>
                </b-list-group-item>
              </b-list-group>
            </b-tab>
            <b-tab title="질문" >
              <b-list-group v-if="!questions.length" flush>
                <b-list-group-item>
                    <span class="text-muted">활동 내역이 없습니다.</span>
                </b-list-group-item>
              </b-list-group>
              <b-list-group v-for="question in questions" :key="question.id" flush>
                <b-list-group-item>
                  "{{ question.title }}" <span class="text-warning">{{ question.createdAt }}</span>
                </b-list-group-item>
              </b-list-group>
            </b-tab>
            <b-tab title="답변">
              <b-list-group v-if="!answers.length" flush>
                <b-list-group-item>
                    <span class="text-muted">활동 내역이 없습니다.</span>
                </b-list-group-item>
              </b-list-group>
              <b-list-group v-for="answer in answers" :key="answer.id" flush>
                <b-list-group-item>
                    "{{ answer.question.title }}" <span class="text-warning">{{ answer.createdAt }}</span>
                </b-list-group-item>
              </b-list-group>
            </b-tab>
            <b-tab title="좋아요">
              <b-list-group v-if="!likes.length" flush>
                <b-list-group-item>
                    <span class="text-muted">활동 내역이 없습니다.</span>
                </b-list-group-item>
              </b-list-group>
              <b-list-group v-for="like in likes" :key="like.id" flush>
                <b-list-group-item>
                    "{{ like.question.title }}" <span class="text-warning">{{ like.createdAt }}</span>
                </b-list-group-item>
              </b-list-group>
            </b-tab>
            <b-tab title="댓글">
              <b-list-group v-if="!comments.length" flush>
                <b-list-group-item>
                    <span class="text-muted">활동 내역이 없습니다.</span>
                </b-list-group-item>
              </b-list-group>
              <b-list-group v-for="comment in comments" :key="comment.id" flush>
                <b-list-group-item>
                    "{{ comment.question.title }}" <span class="text-warning">{{ comment.createdAt }}</span>
                </b-list-group-item>
              </b-list-group>
            </b-tab>
            <b-tab title="Cherry">
              <b-list-group v-if="!logs.length" flush>
                <b-list-group-item>
                    <span class="text-muted">활동 내역이 없습니다.</span>
                </b-list-group-item>
              </b-list-group>
              <b-list-group v-for="log in logs" :key="log.id" flush>
                <b-list-group-item>
                    // TODO
                </b-list-group-item>
              </b-list-group>
            </b-tab>
          </b-tabs>
        </b-col>
      </b-row>
  </div>
</template>

<script>
export default {
  name: 'Profile',
  created () {
    // TODO: from params
    let userId = ''
    this.fetchProfile(userId)
    this.fetchTokens(userId)
    this.fetchQuestions(userId)
    this.fetchAnswers(userId)
    this.fetchLikes(userId)
    this.fetchComments(userId)
  },
  data () {
    return {
      profile: {},
      tokens: 0,
      questions: [],
      answers: [],
      likes: [],
      comments: [],
      logs: []
    }
  },
  methods: {
    fetchProfile (userId) {
      this.profile = {
        name: 'nobody',
        level: 'yellow',
        si: 105
      }
      this.$http.get('/api/users/' + userId)
        .then((response) => {
          this.profile = response.data
        })
    },
    fetchTokens (userId) {
      this.tokens = 10
      this.$http.get('/api/users/' + userId + '/tokens')
        .then((response) => {
          this.tokens = response.data
        })
    },
    fetchQuestions (userId) {
      this.questions = []
      this.$http.get('/api/questions', {
        params: {
          createdBy: userId
        }
      })
        .then((response) => {
          this.questions = response.data
        })
    },
    fetchAnswers (userId) {
      this.answers = []
      this.$http.get('/api/answers', {
        params: {
          createdBy: userId
        }
      })
        .then((response) => {
          this.answers = response.data
        })
    },
    fetchLikes (userId) {
      this.likes = []
      this.$http.get('/api/likes', {
        params: {
          createdBy: userId
        }
      })
        .then((response) => {
          this.likes = response.data
        })
    },
    fetchComments (userId) {
      this.comments = []
    },
    fetchLogs (userId) {
      this.logs = []
      this.$http.get('/api/logs', {
        params: {
          from: userId,
          to: userId
        }
      })
        .then((response) => {
          this.likes = response.data
        })
    }
  }
}
</script>
