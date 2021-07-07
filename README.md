## Requirements

Ansible 2.9+ needs to be installed

```
python3 -m pip install --user ansible
python3 -m pip install --user docker
```

```
ansible-galaxy collection install -r collections/requirements.yml
```

## Boostrapping PTP

1. Make sure your NGC credentials are exported like this:

```
export NGC_KEY='...'
```

To get the API key login ngc.nvidia.com and go to Setup->Generate API Key, press the Generate API Key from the top right corner.

2. Check the input variables and update them to match your environment

```
ip_address: 20.138.1.1/16
ptp_interface: swp12
```

3. Bootstrap PTP 

```
ansible-playbook bootstrap.yml
```

