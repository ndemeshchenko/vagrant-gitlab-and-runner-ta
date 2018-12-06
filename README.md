# vagrant-gitlab-and-runner-ta

Gitlab server and runner setup for Vagrant

## Prerequisites: Install ansible dependency roles

```shell
ansible-galaxy install -r roles.yml
```

## Vagrant provision

```shell
vagrant up

# add vagrant hosts to your ssh config for ansible to be able to contact them
vagrant ssh >> ~/.ssh/config
```


## Run ansible

```shell
ansible-playbook -b -i inventory main.yaml
```

## Access Gitlab

By the time ansible run finished, you should be able access gitlab UI `http://localhost:8080`, you have to setup root password at first login.

During ansible run test repo was imported and you should have it ready along with runner registered and ready to do jobs for this repo.
