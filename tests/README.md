The first test to check that DNS is working on a kubernetes cluster. This does not fix, or disagnose any issues, but will check that the default DNS works in the default namespace and in others.

Based off of:
https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/

Deploy:
```kubectl apply -f dns_test_deployment.yml```

This will create the pods and namespaces used

Test:
1. Can we resolve the default address kubernetes.default?

```kubectl exec -it dnsutils -- nslookup kubernetes.default```

2. Can we resolve a service we created in the default namespace?

```kubectl exec -it dnsutils -- nslookup nginx-service.default```

3. Can we resolve a service in a new namespace?

```kubectl exec -it dnsutils -- nslookup nginx-service-in-ns.test-namespace```

Cleanup:
```kubectl delete -f dns_test_deployment.yml```
