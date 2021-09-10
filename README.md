## Requirements

Ansible 2.10+ needs to be installed:

```
sudo apt update 
sudo apt install python3-pip -y
sudo python3 -m pip install ansible~=2.10
```

Install extra dependencies:

```
sudo python3 -m pip install docker
sudo ansible-galaxy collection install -r collections/requirements.yml
```

## Boostrapping PTP

> Note: the playbook automates all the steps from the DPU Deployment Guide starting from 7.2 `Switch from DPU-embedded mode to SEPERATED_HOST mode`

1. Make sure your NGC credentials are exported like this:

```
export NGC_KEY='...'
```

To get the API key login ngc.nvidia.com and go to Setup->Generate API Key, press the Generate API Key from the top right corner.

2. Make sure you've downloaded the mlxconfig_host.db from the [Rivermax Getting Started page](https://developer.nvidia.com/networking/rivermax-getting-started) and copied the file to the DPU.

3. Check the input variables and update them to match your environment

```
ip_address: 20.138.1.1/16
ptp_interface: p0
mlx_config_path: /home/ubuntu/mlxconfig_host.db
```

4. Update the inventory to match the details of the DPU

The following information will be used by Ansible to SSH into the DPU:

```
$ cat hosts
bluefield ansible_host=172.16.0.190 ansible_user=ubuntu ansible_password=ubuntu
```

5. Bootstrap PTP 

```
ansible-playbook -i hosts -e NGC_KEY=$NGC_KEY bootstrap.yml
```


> Note: by default this playbook will stop if it detects that the mode is not correct. It's possible to make it change the mode and force-reboot the DPU by passing an extra arguments `-e safe=false`