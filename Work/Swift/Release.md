
#### Web App

```bash
## ggpullall
git checkout master && git pull --rebase && git checkout develop && git pull --rebase

git flow release start {{ version number + 0.1 }}

## replace all prev version number to + 0.1

git add .
git commit -m "build: bump version"

# ggpushall
git push origin master && git push origin develop && git push --tags

make beta
make production
```

##### Monitoring Web App
Monitor web app using [Sentry](https://shipx-24.sentry.io/dashboard/default-overview/?project=5567208)

#### Mobile App

```bash
# ggpullall
git checkout master && git pull --rebase && git checkout develop && git pull --rebase

make release
```

##### Expo Application Services (EAS)

1. Build
2. Submit
3. Update


#### Backend

```bash
# ggpullall
git checkout master && git pull --rebase && git checkout develop && git pull --rebase

# find all current version number in vscode and replace the version number with + 0.1

git tags {{ version number + 0.1 }}

git add .
git commit -m "build: bump version"

git push origin develop && git push origin master && git push -t
```


##### Google Cloud Console (GCC)

1. Search `Cloud Build` and check if the api is building the docker image
2. Copy the image url and open `Kubernetes Engine` tab in GCC
3. Roll out the update by scaling up the pod
4. Delete the old pod and ensure only 1 pod is up (scale down)

#### Gateway
If there are changes to GraphQL schema, gateway needs to be restart. To restart gateway:

1. Open `Kubernetes Engine` and click at gateway
2. Scale up the pod to 2 and wait for gateway to complete build new pod
3. Delete old pod and scale down the kubernetes cluster to 1

