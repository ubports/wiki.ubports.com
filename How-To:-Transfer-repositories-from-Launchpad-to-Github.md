### Preparations ###
1. Install bazaar and git cmdline tools according to your OS/Distro
2. Install (if necessary) the following bazaar extension:
    `bzr-fastimport`

### Workflow ###
3. Create an intermediate folder for bazaar and check out the project there:
    `bzr branch lp:<project_name> <origin_folder>`
4. Create an intermediate folder for git and create an empty git repository there:
    `git init <dest_folder>`
5. stream an export of bazaar into git:
    `cd <dest_folder>; bzr fast-export <origin_folder> | git fast-import`
6. Upload full repo to Github:
    `git remote add origin <dest-url.git>`
7. Verify
    `git remote -v`
8. Import to Github:
    `git push origin master`

Voila!