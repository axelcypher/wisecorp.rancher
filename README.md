Ansible Role: Rancher
=========

Installs [Ranhcer](https://rancher.com/) using [helm charts](https://rancher.com/docs/rancher/v2.5/en/installation/install-rancher-on-k8s/).
Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    cert_manager_version: '1.0.4'

Specify the [certmanager](https://rancher.com/docs/rancher/v2.5/en/installation/install-rancher-on-k8s/#4-install-cert-manager) version required by Rancher.

    k3s_kube_config_path: "~{{ ansible_user }}/.kube/config"
Is the path to kubeConfig file to access the kubernetes Cluster where Rancher and its dependencies will be installed.

    rancher_version: '2.5.8'
    rancher_dns_name: rancher.company.com
    rancher_options:
      letsencrypt_email: technique@wisecorp.tn
      ingress_tls_source: letsEncrypt # possible values: rancher, letsEncrypt, secret
      noProxy: 127.0.0.0/8\,.svc\,.cluster.local # possible values: external, ingress
      replicas: 2
      tls: ingress # possible values: external, ingress

Define Rancher installation version and [options](https://rancher.com/docs/rancher/v2.5/en/installation/install-rancher-on-k8s/#5-install-rancher-with-helm-and-your-chosen-certificate-option).

Dependencies
------------

- [gantsign.helm](https://github.com/gantsign/ansible_role_helm)

variables that can be overwritten are 

    # Helm version number
    helm_version: '3.6.0'

    # The CPU architecture of the Helm executable to install
    helm_architecture: 'amd64'

    # Mirror to download Helm from
    helm_mirror: 'https://get.helm.sh'

    # Dir where Helm should be installed
    helm_install_dir: '/usr/local/share/helm'

    # Directory to store files downloaded for Helm
    helm_download_dir: "{{ x_ansible_download_dir | default(ansible_env.HOME + '/.ansible/tmp/downloads') }}"



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - role: slchniguir.rancher

Inside vars/main.yml:

    cert_manager_version: '1.0.4'
    rancher_version: '2.5.8'
    rancher_dns_name: rancher.company.com
    k3s_kube_config_path: "~{{ ansible_user }}/.kube/config"
    rancher_options:
      letsencrypt_email: technique@wisecorp.tn
      ingress_tls_source: letsEncrypt # possible values: rancher, letsEncrypt, secret
      noProxy: 127.0.0.0/8\,.svc\,.cluster.local # possible values: external, ingress
      replicas: 2
      tls: ingress # possible values: external, ingress

License
-------

BSD/MIT

Author Information
------------------

Author: Salem Chniguir <salem.chniguir@wisecorp.tn>
