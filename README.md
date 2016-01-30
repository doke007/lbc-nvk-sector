# lbc-nvk-sector

### Installation

You need oc (https://github.com/openshift/origin/releases) localy installed:

create a new project

```sh
oc new-project lbc-nvk-sector \
    --description="Website - lbc-nvk-sector static" \
    --display-name="Website lbc-nvk-sector.be"
```

#### github private deploy key

create an ssh deploy key without passphrase
```sh
ssh-keygen -f ~/.ssh/lbc-nvk-sector
```

```sh
oc secrets new-sshauth lbc-nvk-sector --ssh-privatekey=/home/joeri/.ssh/lbc-nvk-sector
oc secrets add serviceaccount/builder secrets/lbc-nvk-sector
```

Clone the repository
```sh
git clone git@github.com:doke007/lbc-nvk-sector.be.git
cd lbc-nvk-sector.be
```

Create the BuildConfig

```sh
oc create -f BuildConfig.yaml
```
Add your key to the deploy keys of you repository on GitHub

```sh
cat ~/.ssh/lbc-nvk-sector.pub
```

Deploy from private git repository

```sh
oc new-app git@github.com:doke007/lbc-nvk-sector.be.git
```

#### route.yml

Routes to a static hostname

```sh
oc create -f Route.yaml
```
#### WebHooks

You can find the (github and generic) webhook in the openshift control pannel ! (Browse - Builds)
You can copy the url to clipboard and paste it in Github webhook url (handy for rolling updates)
