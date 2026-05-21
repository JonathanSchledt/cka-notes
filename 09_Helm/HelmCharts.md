# Helm Charts

## Concept

Chart directory structure:

- templates (directory)
- values.yaml
- Chart.yaml
- LICENSE
- README.md
- charts (directory, may contain dependencies)

## Key Commands

```bash
helm create mychart

helm install myrelease ./mychart

helm install myrelease ./mychart -f custom-values.yaml

helm show chart bitnami/wordpress

helm show values bitnami/wordpress
```

## Minimal YAML Example

```yaml
# Chart.yaml
apiVersion: v2 # helm 3
appVersion: 5.8.1
version: 12.1.27
name: wordpress
description: Web publishing platform for building blogs and websites.
type: application
dependencies:
  - condition: mariadb.enabled
    name: mariadb
    repository: https://charts.bitnami.com/bitnami
    version: 9.x.x
keywords:
  - application
  - blog
  - wordpress
maintainers:
  - email: containers@bitnami.com
    name: Bitnami
home: https://github.com/bitnami/charts/tree/master/bitnami/wordpress
icon: https://bitnami.com/assets/stacks/wordpress/img/wordpress-stack-220x234.png

# deployment.yaml
apiVersion: {{ include "apiVersion" . }}
kind: Deployment
metadata:
  name: {{ include "common.names.fullname" . }}
  namespace: {{ .Release.Namespace | quote }}
  labels: {{- include "common.labels.standard" . | nindent 4 }}
spec:
  selector:
    matchLabels: {{- include "common.labels.matchLabels" }}
  replicas: {{ .Values.replicaCount }}
  {{- end }}
  template:
spec:
  containers:
    - name: wordpress
      image: {{ template "wordpress.image" . }}
      env:
        - name: WORDPRESS_DATABASE_NAME
          value: {{ include "wordpress.databaseName" . | quote }}
        - name: WORDPRESS_DATABASE_USER
          value: {{ include "wordpress.databaseUser" . | quote }}
        - name: WORDPRESS_USERNAME
          value: {{ .Values.wordpressUsername | quote }}
        - name: WORDPRESS_PASSWORD
          valueFrom:
            secretKeyRef:
              name: {{ include "wordpress.secretName" . }}
              key: wordpress-password
        - name: WORDPRESS_BLOG_NAME
          value: {{ .Values.wordpressBlogName | quote }}

# values.yaml
image:
  registry: docker.io
  repository: bitnami/wordpress
  tag: 5.8.2-debian-10-r0
## @param wordpressUsername WordPress username
##
wordpressUsername: user
## @param wordpressPassword WordPress user password
## Defaults to a random 10-character alphanumeric string if not set
##
wordpressPassword: ""
## @param existingSecret
##
existingSecret: ""
## @param wordpressEmail WordPress user email
##
wordpressEmail: user@example.com
## @param wordpressFirstName WordPress user first name
##
## @param wordpressBlogName Blog name
##
wordpressBlogName: User's Blog!
```
