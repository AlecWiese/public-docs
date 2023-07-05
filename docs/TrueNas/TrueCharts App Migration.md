#TrueNas #truecharts 
#### [PVC Migration Script | TrueCharts](https://truecharts.org/manual/SCALE/guides/pvc-migration-script/)
**Credit**
This guide uses the [HeavyBullets Migration Guide for PVCs](https://github.com/Heavybullets8/TT-Migration) so credit for this one goes there, also to [Zasx](https://github.com/ZasX) from the [TrueCharts](https://www.truecharts.org) team for the steps used to create these guides/scripts


I frequently found I was getting the error message when running the script between removing the old chart, and trying to complete setup of the new version.  Setup B has been modified to note the command needed to resolve this . (credit ksimm1 from the TrueCharts discord for that)
```
[EFAULT] Failed to install chart release: Error: INSTALLATION FAILED: unable to build kubernetes objects from release manifest: resource mapping not found for name: "lldap" namespace: "" from "": no matches for kind "PodMonitor" in version "monitoring.coreos.com/v1" ensure CRDs are installed first
```

Migration Steps[​](https://truecharts.org/manual/SCALE/guides/pvc-migration-script/#migration-steps)
----------

1. First things first create a directory inside a dataset that's NOT `ix-applications`, for this guide I used `migration`

2. Clone the `Heavybullets Migration Git Repo`

```
git clone https://github.com/Heavybullets8/TT-Migration.git
```

3. Go to the `TT-Migration` sub-directory and excute

4. Follow prompts
   a. Choose Application (for example `filebrowser`)
   <img alt="Copy Config" src="https://truecharts.org/assets/images/Copy-App-Config-2e39a5cead9f8bf6338f04c3120f8854.png" width="800" />
   
   b. Once that's done press `x` and continue to the next screen. Before installing the new application, remove the old namespace. 
   ```sh
k3s kubectl get namespace "ix-<app>" -o json \
  | tr -d "\n" | sed "s/\"finalizers\": \[[^]]\+\]/\"finalizers\": []/" \
  | k3s kubectl replace --raw /api/v1/namespaces/ix-<app>/finalize -f -
   ```
	   credit ksimm1 from the TrueCharts discord

  c.  install the new Application
   <img alt="New App Install" src="https://truecharts.org/assets/images/New-App-Config-e1279cace7428e0213b997af4b88e20e.png" width="800" />
   d. Watch the app finish

5. Enjoy new app

### Note[​](https://truecharts.org/manual/SCALE/guides/pvc-migration-script/#note) ###

If an application fails to stop the NEW application, and throws any errors. You can attempt to run the script again, with:

```sh
bash migrate.sh -s
```

which will skip to the step immediately after deleting the old application.