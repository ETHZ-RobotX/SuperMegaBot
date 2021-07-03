---
layout: default
title: Update Core Software
parent: SMB Core Software
nav_order: 4
nav_exclude: true
---

## Update the SMB Core Software
If some packages were updated on Github you need to pull the latest changes.

```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Pull the latest changes
vcs pull
```
## Import new repositories
In some cases there might be new repositories needed in order to use the SMB. Check the [smb.repos](https://github.com/ETHZ-RobotX/SuperMegaBot/blob/master/smb.repos) file.

If this is the case
```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Add the new repositories
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .

# Pull the latest changes
vcs pull
```

## Troubleshooting

### Path already exists
If you import the repositories you might encounter this error:

```bash
Path already exists and contains a different repository
```

This means that the repository on your host is outdated and the URL of the new one is changed. In this case just delete the folder and execute again the import command

```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Delete outdated repository
rm -rf <outdated_repository>

# Add the new repositories
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .

# Pull the latest changes
vcs pull
```

### Build failed
Sometimes the name of the repository could change, and if you try to build again than you will receive the following error:

```bash
CMake Error: The source directory "/path/to/directory" does not exist.
```

In this case just clean the your builds and build again.
```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/

# Clean
catkin clean <package_name>

# Build
catkin build <package_name>
```