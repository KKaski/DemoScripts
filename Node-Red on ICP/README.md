# Node-Red on ICP
This demo is based on the description here
https://medium.com/@noazdad/adding-the-nodered-service-to-the-ibm-cloud-private-catalog-7a3c5a9c09d9

ICP the DNS loopback was enabled by editing config.yaml file

```
## Allow loopback dns server in cluster nodes
loopback_dns: true
```

The readiness and liveness probeneeds to be modified in order to work with kubernetes. 

```
spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          imagePullPolicy: {{ .Values.image.pullPolicy }}
          ports:
            - name: http
              containerPort: 1880
              protocol: TCP
          livenessProbe:
            httpGet:
              path: /
              port: 1880
          readinessProbe:
            httpGet:
              path: /
              port: 1880
``` 

All the steps has been done you can add the chart to your catalog by running

bx pr load-helm-chart  --archive node-red-0.1.1.tgz

