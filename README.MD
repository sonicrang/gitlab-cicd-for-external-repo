## 极狐GitLab用于外部仓库的 CI/CD

详见文档：https://docs.gitlab.cn/jh/ci/ci_cd_for_external_repos/#limitations

### 功能
- 可链接外部仓库，如GitHub、或其他Git仓库并使用GitLab CI/CD
- 本质是通过GitLab Pull Mirror从外部仓库定时拉取代码，然后读取GitLab CI脚本如`.gitlab-ci.yml`运行
- 与GitHub的集成效果较好，可在GitHub中通过PR触发GitLab CI，可在GitHub PR中查看GitLab CI的状态

### 限制
- 不能直接使用外部仓库，需要通过Mirror同步代码，但同步的内容禁用了议题、合并请求、wiki 和代码片段等，是个轻量级项目
- Mirror有时间间隔，理论上不是实时触发
- 从Fork仓库发起PR不会触发GitLab CI，从其他Git仓库（非GitHub）发起PR不会触发GitLab CI
- 由于是Mirror，本质上还是需要在外部仓库编写并管理GitLab CI脚本如`.gitlab-ci.yml`

### 操作流程

1. 在GitHub中创建Personal Token，选择`repo`和`admin:repo_hook`
   ![image](https://user-images.githubusercontent.com/5936153/207013449-53282690-5d1a-41d5-b39b-5d49dd8c3889.png)
2. 在GitHub中创建`.gitlab-ci.yml`，如
   ![image](https://user-images.githubusercontent.com/5936153/207014541-c1d41db9-1184-408b-b472-bcff46b988cf.png)
3. 在GitLab中新建项目，选择“为外部仓库运行CI/CD”
   ![image](https://user-images.githubusercontent.com/5936153/207013329-cda9810a-d535-444e-82f8-73c59b810331.png)
4. 输入GitHub Personal Token，选择需要连接的项目，修改路径，点击“连接”
   ![image](https://user-images.githubusercontent.com/5936153/207015062-57604097-76b9-4744-b2da-d5b8294409b7.png)
   ![image](https://user-images.githubusercontent.com/5936153/207015078-dda09af6-cb89-4c2e-a3e6-e69ed61e18ec.png)
5. 在GitHub中修改文件或发起PR，等待同步完成后GitLab会自动运行CI，在GitHub的PR中可查看GitLab CI运行状态和结果
   ![image](https://user-images.githubusercontent.com/5936153/207015233-9e7490fd-1139-436b-bb54-38450f8f1c2d.png)
