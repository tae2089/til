internal nlb를 만드는 작업을 진행했다.

해당 작업을 하면서 테스트해본것은 다음과 같다.

nlb에 경우 eks load balancer를 활용해서 만들었다.

## 진행 내용

1. 외부에서도 호출하면 연결이 가능한지에 대한 테스트
   - 이 테스트에 경우 내 로컬에서 도커를 활용해서 nlb와 연결해보는 테스트를 진행했다.
   - 결과적으로 연결이 되지 않아 내가 원했던 테스트가 정상적으로 되었다.
2. nat gateway가 없더라도 연결이 가능한지에 대한 테스트
   - 이 테스트는 nat gateway를 router table에서 제거하고 진행했다.
   - 서버와 통신이 되는 것을 확인했고 vpc peering을 통해서 진행된것으로 확인했다.

## 관련 코드

```yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: external
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: ip
    service.beta.kubernetes.io/aws-load-balancer-scheme: internal
  labels:
    app: redis-cluster
  name: redis-cluster-loadbalancer
  namespace: db
spec:
  ports:
    - port: 6379
      protocol: TCP
      targetPort: 6379
      name: redis
  selector:
    app.kubernetes.io/name: redis-cluster
  type: LoadBalancer
```

여기서 aws-load-balancer-scheme가 internal이어야만이 정상동작한다.
iprange 설정을 할 수도 있지만 그거는 하지 않았다. 내부에서만 동작하기에 필요없어보였다.
