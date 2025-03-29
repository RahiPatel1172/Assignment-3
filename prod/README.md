# Production Environment Setup

This directory contains the Kubernetes configurations for deploying Gitea with MySQL in a production environment.

## Prerequisites

- Kubernetes cluster
- kubectl configured
- Ansible installed
- Python with pip
- ngrok account with a custom domain

## Virtual Machine Information
- IP Address: 10.172.27.12
- Login: ubuntu/Secret55

## Directory Structure

```
prod/
├── down.yaml        # Teardown script
├── mysql.yaml       # MySQL k8s manifests
├── gitea.yaml       # Gitea k8s manifests
├── up.yaml          # Setup script
└── README.md        # This file
```

## Deployment

1. Deploy the environment:
   ```bash
   ansible-playbook up.yaml
   ```

2. Verify the deployment:
   ```bash
   kubectl get pods
   kubectl get services
   ```

3. Set up ngrok exposure:
   ```bash
   cd ../ngrok
   ansible-playbook up.yaml
   ```

4. Access Gitea:
   - The Gitea service will be available at: https://your-subdomain.ngrok-free.app
   - Access Adminer (MySQL management) on port 8080

## Teardown

To remove the deployment:
```bash
ansible-playbook down.yaml
```

## Security Notes

- The current configuration uses basic passwords. In a production environment:
  - Use Kubernetes secrets for sensitive data
  - Update MySQL to a newer version
  - Configure proper authentication and authorization
  - Enable HTTPS/TLS
  - Set up proper backup procedures

## Maintenance

- Monitor the persistent volumes for storage usage
- Regularly backup the MySQL database
- Keep the Gitea and MySQL images updated

## External Access

The Gitea instance is exposed via ngrok at: https://9615-2a09-bac1-14a0-238-00-2ac-4d.ngrok-free.app
This URL was obtained from the lab machine (10.172.27.12) in week 9-11.
Please replace "your-subdomain" with your actual ngrok subdomain from the lab machine. 