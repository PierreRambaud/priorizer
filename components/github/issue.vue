<template>
    <li class="list-group-item js-notification js-navigation-item unread issue-notification" aria-selected="false">
        <a class="list-group-item-link" :href="issue.html_url" :title="issue.title" target="_blank">
            <span :class="[iconState]" class="type-icon tooltipped tooltipped-w">
                <svg v-if="isIssue" class="octicon octicon-issue-opened" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true">
                    <path fill-rule="evenodd" d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7s-2.56 5.7-5.7 5.7A5.71 5.71 0 0 1 1.3 8c0-3.14 2.56-5.7 5.7-5.7zM7 1C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7-3.14-7-7-7zm1 3H6v5h2V4zm0 6H6v2h2v-2z"/>
                </svg>

                <svg v-if="isPullRequest" class="octicon octicon-git-pull-request" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true">
                    <path fill-rule="evenodd" d="M11 11.28V5c-.03-.78-.34-1.47-.94-2.06C9.46 2.35 8.78 2.03 8 2H7V0L4 3l3 3V4h1c.27.02.48.11.69.31.21.2.3.42.31.69v6.28A1.993 1.993 0 0 0 10 15a1.993 1.993 0 0 0 1-3.72zm-1 2.92c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zM4 3c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v6.56A1.993 1.993 0 0 0 2 15a1.993 1.993 0 0 0 1-3.72V4.72c.59-.34 1-.98 1-1.72zm-.8 10c0 .66-.55 1.2-1.2 1.2-.65 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/>
                </svg>
            </span>
            <span class="list-group-item-name">
                {{ issue.title }}
            </span>
            <span class="list-group-item-time" v-if="updated_at">
                <timeago :datetime="updated_at" :auto-update="30"/>
            </span>
        </a>
    </li>
</template>

<script>
  import constant from '~/constant';

  export default {
    name: 'notification',
    props: {
      issue: {
        type: Object,
        required: true,
      },
      type: {
        type: String,
        required: false,
      },
      updated_at: {
        type: String,
        required: false,
      },
    },
    computed: {
      isPullRequest() {
        return this.type === constant.ISSUE_TYPE.PR;
      },
      isIssue() {
        return this.type === constant.ISSUE_TYPE.ISSUE;
      },

      iconState() {
        if (this.issue.merged) {
          return 'type-icon-state-merged';
        }

        return `type-icon-state-${this.issue.state}`;
      },
    },
  };
</script>

<style lang="scss">
</style>
