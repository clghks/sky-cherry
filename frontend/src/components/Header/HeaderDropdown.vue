<template>
  <AppHeaderDropdown right no-caret>
    <template slot="header">
      <img
        src="/static/img/avatars/profile_thumbnail.jpg"
        class="img-avatar" />
    </template>
    <template slot="dropdown">
      <b-dropdown-item>
        <i class="fa fa-search" /> 질문검색
      </b-dropdown-item>
      <b-dropdown-item>
        <i class="fa fa-quora" /> 질문하기
      </b-dropdown-item>
      <b-dropdown-item>
        <i class="fa fa-bitcoin" /> Cherry Transfer
      </b-dropdown-item>
      <b-dropdown-item>
        <i class="fa fa-bell-o" /> 알림
        <!-- <b-badge variant="info">10</b-badge> -->
      </b-dropdown-item>
      <b-dropdown-item>
        <i class="fa fa-user-o" /> 프로필
      </b-dropdown-item>
    </template>
  </AppHeaderDropdown>
</template>

<script>
import { HeaderDropdown as AppHeaderDropdown } from '@coreui/vue'
export default {
  name: 'HeaderDropdownAccnt',
  components: {
    AppHeaderDropdown
  },
  data () {
    return {}
  }
}
</script>
