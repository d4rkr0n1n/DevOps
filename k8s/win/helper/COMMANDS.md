For first 10: 
kubectl describe pods |  Select-Object -First 10

kubectl describe pods | Select-String "Node" | Select-Object -First 10