# Troubleshooting

## Build fails with 403 on push
- Go to Settings -> Actions -> General
- Set workflow permissions to "Read and write permissions"

## Image tag must be lowercase
- GitHub usernames with capitals cause this
- The workflow handles it automatically, but your username in manifests must be lowercase

## Pod stuck in Pending
- Check `kubectl describe pod <pod-name> -n <yourname>-paper`
- Usually a resource quota issue or PVC not binding

## Pod in CrashLoopBackOff
- Check logs: `kubectl logs <pod-name> -n <yourname>-paper`
- Common causes: missing configmap mount, not enough memory

## ArgoCD app stuck in OutOfSync
- Check the ArgoCD UI for diff details
- Make sure namespace in Application matches your manifests

## Can't connect to Minecraft server
- Verify your Gateway port assignment
- Check `kubectl get gateway -n <yourname>-paper`
- Try `kubectl port-forward svc/<yourname>-paper 25565:25565 -n <yourname>-paper` to test locally first