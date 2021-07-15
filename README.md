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

4. Bootstrap PTP 

```
ansible-playbook bootstrap.yml
```

If running as sudo use this command:

```
NGC_KEY=$NGC_KEY sudo -E ansible-playbook bootstrap.yml
```
