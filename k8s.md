
| master  | 168.138.12.7    | 10.0.0.17  |
| ------- | --------------- | ---------- |
| worker1 | 207.211.148.223 | 10.0.0.65  |
| worker2 | 207.211.157.226 | 10.0.0.209 |
Join Command: ```
kubeadm join 10.0.0.17:6443 --token qkpkbn.yys2dcdmtiyk6dgt \
        --discovery-token-ca-cert-hash sha256:17c3e6b24674789e6be8f7e77637b22f35896332d63d61c3c9932c87241f8e00
```
118.138.238.161:8089