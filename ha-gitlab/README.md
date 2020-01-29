# Semi high available Gitlab setup with Ansible

# Architecture

- Gitab 1 
  - Gitlab
  - Glusterfs Client
- Gitlab 2 
  - Gitlab
  - Glusterfs Client
- PRG 1 
  - PostgreSQL Master
  - Redis Master
  - Glusterfs Server
- PRG 2
  - PostgreSQL Slave
  - Redis Slave
  - Glusterfs Server
- PRG 3
  - Glusterfs Server

Requires external loadbalancer


#### Dynamic variables are stored in the `group_vars` directory

#### Add your SSL cert here: 
`./roles/common/ssl/ssl.key`
`./roles/common/ssl/ssl.crt`

# Run all the playbooks
```bash
ansible-playbook site.yml -i hosts
```
This will install Gitlab, PSQL, Redis, Gluster

# Deploy Gitlab
```bash
ansible-playbook gitlab.yml -i hosts
```

# Deploy Postgres
```bash
ansible-playbook postgresql.yml -i hosts
```

# Deploy Redis
```bash
ansible-playbook redis.yml -i hosts
```

# Deploy GlusterFS
```bash
ansible-playbook glusterfs-server.yml -i hosts
```
