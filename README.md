Ansible Role: Gitea Git Server on OpenShift
=========

Ansible Role for deploying Gitea Server on OpenShift. This role creates an admin 
account, a user account and also if configured would generate the specified number of user 
accounts for gitea.


Role Variables
------------

| Variable                  | Default Value   | Description   |
|---------------------------|-----------------|---------------|
|`gitea_service_name`        | gitea            | gitea service name on OpenShift  |
|`gitea_image_version`       | 1.7.0         | gitea image version as available on [Docker Hub](https://hub.docker.com/r/gitea/gitea/tags) |
|`gitea_route`               | gitea-{{ project_name }}.127.0.0.1.nip.io | **Required**. gitea hostname to be configure |
|`gitea_admin_user`          | gitea            | Admin account username |
|`gitea_admin_password`      | gitea            | Admin account password |
|`gitea_user`                | developer       | User account username |
|`gitea_password`            | developer       | User account password |
|`gitea_generate_user_count` | 0               | Number of users accounts to generate with the user account password |
|`gitea_generate_user_format`| demouser%02d        | [printf style format](https://en.wikipedia.org/wiki/Printf_format_string) to use for generating user accounts |
|`max_mem`                  | 2Gi             | Max memory allocated to gitea container |
|`min_mem`                  | 512Mi           | Min memory allocated to gitea container |
|`max_cpu`                  | 1               | Max cpu allocated to gitea container |
|`min_cpu`                  | 200m            | Min cpu allocated to gitea container |
|`clean_deploy`             | false           | Deploy a fresh gitea and delete the existing one if any |
|`project_name`             | gitea            | OpenShift project name for the gitea container  |
|`project_display_name`     | Gitea            | OpenShift project display name for the gitea container  |
|`project_desc`             | Gitea Git Server | OpenShift project description for the gitea container |
|`project_admin`            | -               | If set, the user to be assigned as project admin |
|`project_annotations`      | -               | OpenShift project annotations for the gitea container |
|`openshift_cli`            | oc              | OpenShift CLI command and arguments (e.g. auth)       | 

OpenShift Version Compatibility
------------
When listing this role in `requirements.yml`, make sure to pin the version of the role via one of the tags:

```
- src: samrostampour.openshift_gitea
  version: 1.0.0
```  

The following tables shows the version combinations that are tested and verified:

| Role Version      | OpenShift Version |
|-------------------|-------------------|
| 1.1.x   | 3.9.x, 3.10.x, 3.11.x |



Example Playbook
------------

```
name: Example Playbook
hosts: localhost
tasks:
- import_role:
    name: samrostampour.openshift_gitea
  vars:
    gitea_route: "gitea-cicd-project.apps.myopenshift.com"
    project_name: "cicd-project"
    gitea_generate_user_count: "2"
    openshift_cli: "oc --server http://master:8443"
```