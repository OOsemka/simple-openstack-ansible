# Simple Example of creating Ansible playbook to OpenStack with shade libraries
This can be used either from Ansible Core or Ansible Tower. 
Simply import it to your ansible server and modify variables under vars/ to match your environment. Each variable has been augmented with descriptive comments

If you use Ansible Tower make sure you set up your credentials that matches a keypair in OpenStack. 
It is also a good idea to use extra_vars field for dynamic variables rather then yml file. Simply copy the content of vars/create-dynamic-vars.yml into extra_vars field.

# What are the playbooks
create-workload.yml is a simple playbook that creates an instance and installs a list of packages. Both instance attributes and the list of packages can be set up in :
ansible/vars/create-dynamic-vars.yml

delete-workload.yml - is a single task playbook that deletes the OpenStack instance .. should be used with the same variables as create-workload.yml

# Example of launching workloads from tower API

Launch a workload via API:

curl -f -H 'Content-Type: application/json' -XPOST --user admin:<secret>   https://<tower_ip>/api/v2/job_templates/7/launch/ --insecure


Delete workload with API:

curl -f -H 'Content-Type: application/json' -XPOST --user admin:<secret> https:///<tower_ip>/api/v2/job_templates/8/launch/ --insecure


Create with custom variables:

curl -f -H 'Content-Type: application/json' -XPOST --user admin:<secret> -d '{"extra_vars": "{\"instance_name\": \"from_api\"}"}'   https:///<tower_ip>/api/v2/job_templates/7/launch/ --insecure


Please note in my case job_template 7 has been used for create_workload.yml where job_template 8 is for delete_workload.yml
You might also want to enable 'PROMPT ON LAUNCH' for the extra_vars inside the Tower
