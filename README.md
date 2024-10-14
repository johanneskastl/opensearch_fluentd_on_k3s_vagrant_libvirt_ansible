# opensearch_fluentd_on_k3s_vagrant_libvirt_ansible

Vagrant-libvirt setup that creates a VM with [k3s](https://k3s.io/), the minimal
lightweight Kubernetes distribution.

On top of k3s, this setup installs [OpenSearch](https://opensearch.org/) with
[Fluentd](https://www.fluentd.org/).  It also installs an instance of Nginx and
a MinIO instance, just to have some workload in the cluster.

Default OS is openSUSE Leap 15.6, but that can be changed in the Vagrantfile.
Please be aware, that this might break the Ansible provisioning.

## Vagrant

1. You need `vagrant`, obviously. And `git`. And Ansible...
1. Fetch the box, per default this is `opensuse/Leap-15.6.x86_64`, using
   `vagrant box add opensuse/Leap-15.6.x86_64`.
1. Make sure the git submodules are fully working by issuing
   `git submodule init && git submodule update`
1. Run `vagrant up`
1. Open the URL, that Ansible printed out near the end of the provisioning, and
   log in using the  user 'admin' with password 'totallynotsecurE1@'. The URL
   should look something like `http://opensearch.192.0.2.13.sslip.io`.
1. After dismissing the lots of popups and questions, including selecting the
   "Global" tenant, go to the menu on the left and select **Discover**. Add a
   new index pattern using `logstash-*` as the pattern. After adding the
   pattern, head back to **Discover** and you should see lots of logs.
1. Party!

## Cleaning up

The VMs can be torn down after playing around using `vagrant destroy`. This will
also remove the kubeconfig file `ansible/k3s-kubeconfig`.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via git@johannes-kastl.de
