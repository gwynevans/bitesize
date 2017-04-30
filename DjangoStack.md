[Index](./)
---
# Django Stack

 
* [Provisioning django application using ansible](https://krzysztofzuraw.com/blog/2017/provisioning-django-application-ansible.html)
* [Custom Vagrant box for jump-starting Django projects using Cookiecutter](http://kappataumu.com/articles/vagrant-box-django-cookiecutter-quickstart.html)

---

* [Setting up Django with Nginx, Gunicorn, virtualenv, supervisor and PostgreSQL](http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtuale)
   - Combines Nginx, Gunicorn, virtualenv, supervisord and PostgreSQL into a Django server running on Linux
* https://github.com/jcalazan/ansible-django-stack
   * Ansible Playbook based on the above for setting up a Django app with Nginx, Gunicorn, PostgreSQL, Celery, RabbitMQ, Supervisor, Virtualenv, and Memcached. A Vagrantfile for provisioning a VirtualBox virtual machine is included as well.
       * Needed to ensure was running latest pip
      * Needed to manually install nginx in vagrant vm when ansible failed
* https://github.com/postrational/hello_django  
   - Simple Django project for demo purposes

## Plans
1. Vagrant VM provisioned manually via ssh
2. Vagrant VM provisioned via shell
3. Vagrant VM provisioned via Ansible

* Try [Provisioning Azure boxes with Vagrant](https://unindented.org/articles/provision-azure-boxes-with-vagrant/)
