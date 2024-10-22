# Ansible Role: ECR Container Build

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

An Ansible Role that installs builds Docker container images and (optionally) pushes them to AWS ECR Repositories.

## Requirements

  - Docker
  - Pip packages: `boto3`, `docker`

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ecr_image_src_dir: ../my-project
    ecr_image_name: namespace/my-project

A source directory containing a Dockerfile and any required resources, and the image name (typically in the form `namespace/project`) for the docker image that is built.

    ecr_image_buildargs: {}

Build args to pass to the `docker_image` module when building the Docker image. Args should be passed as an object with key-value pairs, e.g. `{ name: value, name2: value2 }`

    ecr_image_tags: ['latest']

The tags to apply to the final image which is pushed to ECR.

    ecr_login_required: false

Set this to `true` if you are using ECR as the source for your container build (e.g. `FROM` in `Dockerfile`).

    ecr_push: true

Whether to push the built image to ECR. Set to `false` if you're just testing the image build portion or you cannot connect to ECR.

    ecr_region: us-east-1
    ecr_account_id: '123456789012'
    ecr_url: "{{ ecr_account_id }}.dkr.ecr.{{ ecr_region }}.amazonaws.com"

AWS account details for ECR.

## Dependencies

None.

## Example Playbook

Building locally (assuming you already have Docker CE and the `docker` pip package installed):

    ---
    - hosts: localhost
      connection: local
      gather_facts: false
    
      vars:
        ecr_image_src_dir: ../my-project
        ecr_image_name: namespace/my-project
        ecr_image_tags: ['latest','1.2.3']
        ecr_account_id: '123456789012'
        pip_install_packages: ['docker']

      roles:
        - role: nholuong.ecr_container_build


Building on a remote server:

    ---
    - hosts: localhost
      connection: local
      gather_facts: false
    
      vars:
        ecr_image_src_dir: ../my-project
        ecr_image_name: namespace/my-project
        ecr_image_tags: ['latest','1.2.3']
        ecr_account_id: '123456789012'
        pip_install_packages: ['docker']
    
      roles:
        - role: nholuong.docker
        - role: nholuong.pip
        - role: nholuong.ecr_container_build

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟