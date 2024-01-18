## Retrieve superuser password for connecting

```bash
PASSWORD=$(kubectl get secret my-db --template '{{ printf "%s" (index .data "superuser-password" | base64decode) }}')
echo "user: superuser"
echo "user: postgres"
echo "password: $PASSWORD"
```

		