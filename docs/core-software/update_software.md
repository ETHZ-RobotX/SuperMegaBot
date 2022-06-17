---
layout: default
title: Updating Core Software
parent: SMB Core Software
nav_order: 5
---
# Updating the SMB Core Software
The repositories containing the SMB Core software will most likely be updated. It is recommended to update the sofware from time to time.
{: .smb-info}


* Table of contents
{:toc}

## Downloading updates
To download the most recent software, execute the following commands.
```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Add the new repositories
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .

# Pull the latest changes
vcs pull

# Update dependencies with rosdep
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
```

## Build updated packages
While pulling the repositories you might see this message
```bash
Updating <old_commit>..<new_commit>
```

If this is the case you need to build the packages in the respective repository again.

## Troubleshooting

### Path already exists
If you import the repositories you might encounter this error:

```bash
Path already exists and contains a different repository
```

This means that the repository on your host is outdated and the URL of the new one is changed. In this case just delete the folder and execute again the import command.

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
