### Preparations ###
1. Install bazaar and git cmdline tools according to your OS/Distro
2. Install (if necessary) the following bazaar extension:

### Workflow ###
3. Create an intermediate folder for bazaar and check out the project there:
    mkdir <origin_folder>; bzr branch lp:<project_name>
4. Create an intermediate folder for git and create an empty git repository there:
    mkdir <dest_folder>; git init <dest_folder>
5. stream an export of bazaar into git:
    bzr fast-export <origin_folder> | git fast-import <dest_folder>
6. Upload full repo to Github:
    cd <dest_folder>; git remote add origin <dest-url.git>
7. Verify
    git remote -v
8. Import to Github:
    git push origin master

Voila!