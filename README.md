### Download terraform
```
$ curl -sL https://releases.hashicorp.com/terraform/0.12.4/terraform_0.12.4_linux_amd64.zip -O bin
$ unzip bin/terraform_0.12.4_linux_amd64.zip -d bin
$ export PATH=${PWD}/bin:${PATH}
```

### Clone roles
```
$ GIT_SSL_NO_VERIFY=true ansible-galaxy install --force --ignore-errors -r requirements.yml
```

### OST commands
- Get available image list
    ```
    $ openstack --insecure image list
    ```

### Previous steps

* Populate ```vault/secrets.yml``` file with needed user/password info

    * Decrypt file

        ```
        ansible-vault decrypt vault/secrets.yml
        ```

    * Edit information

    * Encrypt file

        ```
        ansible-vault encrypt vault/secrets.yml
        ```

### Execute deployment playbooks
```
$ ansible-playbook playbooks/00-create.yml
$ ansible-playbook playbooks/01-python-setup.yml
$ ansible-playbook playbooks/04-elk-gen-certificates.yml
$ ansible-playbook playbooks/05-elk-stack-kibana.yml --ask-vault-pass
```

### SSH connection
```
$ ssh -i ./ssh/keys/default.pem -o ProxyCommand="ssh -i ./ssh/keys/default.pem -W %h:%p ec2-user@52.209.183.156" ec2-user@10.5.0.11
```