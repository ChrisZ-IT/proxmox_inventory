# proxmox_inventory

An Ansible dynamic inventory that uses the proxmox plugin.

## Required vars
These can be set as env vars or if you run AAP just create a custom Credential type
1. `PROXMOX_URL`: https://{{ proxmox_host }}:8006
2. `PROXMOX_USER`: "{{ username }}"
3. `PROXMOX_PASSWORD`: "{{ password }}" - Optinal: if you an api token 
4. `PROXMOX_TOKEN_ID`: '{{ token_id }}' - Optional: if you use a password
5. `PROXMOX_TOKEN_SECRET`: '{{ api_token }}' - Optional: if you use a password

## Custom Credential Type
### Input configuration
```
fields:
  - id: proxmox_host
    type: string
    label: Proxmox hostname/IP
    help_text: 'env var: PROXMOX_URL'
  - id: username
    type: string
    label: username
    secret: false
    help_text: 'env var: PROXMOX_USER'
  - id: token_id
    type: string
    label: Token id
    secret: false
    help_text: 'env var: PROXMOX_TOKEN_ID, Required if password not provided'
  - id: api_token
    type: string
    label: API Token
    secret: true
    help_text: 'env var: PROXMOX_TOKEN_SECRET, Required if password not provided'
  - id: password
    type: string
    label: Password (optinal)
    secret: true
    help_text: 'env var: PROXMOX_PASSWORD, Required if api id/token not provided'
required:
  - proxmox_host
  - username
```
### Injector configuration
```
env:
  PROXMOX_URL: https://{{ proxmox_host }}:8006
  PROXMOX_USER: '{{ username }}'
  PROXMOX_PASSWORD: '{{ password }}'
  PROXMOX_TOKEN_ID: '{{ token_id }}'
  PROXMOX_TOKEN_SECRET: '{{ api_token }}'
```