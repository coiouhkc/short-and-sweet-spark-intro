## Extract commits from repo
```python
# Note: standard Ubuntu version of GitPython (python3-git:3.1.37-3) does not support Files_TD#change_type, need to use venv.
 
import sys
from git import Repo
 
repo = Repo(sys.argv[1] if len(sys.argv) > 1 else './')
 
commits = repo.iter_commits()
 
print("commit-hash, commit-authored-datetime, commit-author-email, commit-committed-datetime, commit-committer-email, file-name, file-insertions, file-deletions")
 
for commit in commits:
    commit_stats = commit.stats
    for file in commit_stats.files.keys():
        file_stats = commit_stats.files.get(file)
        print(f"{commit.hexsha}, {commit.authored_datetime.isoformat()}, {commit.author.email}, {commit.committed_datetime.isoformat()}, {commit.committer.email}, {file}, {file_stats['insertions']}, {file_stats['deletions']}, {file_stats['change_type']}")
```

## Start jupyter spark
```shell
docker run --rm -it -p 4040:4040 -p 8888:8888 -v "${PWD}":/home/jovyan quay.io/jupyter/pyspark-notebook
```