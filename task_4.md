
# Homework Task #4

_**1. Create users deploy_view and deploy_edit. Give the user deploy_view rights only to view deployments, pods. Give the user deploy_edit full rights to the objects deployments, pods.**_

**Create private key for users deploy_view, deploy_edit:**

openssl genrsa -out deploy_view.key 2048

openssl genrsa -out deploy_edit.key 2048
