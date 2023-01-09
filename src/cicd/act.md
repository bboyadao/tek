## ACT

[https://github.com/nektos/act](https://github.com/nektos/act)

Github-action does not support locally as `gitlab-runner exec ...` like [this](https://gitlab.com/gitlab-org/gitlab-runner).

So this tool is play ground at the local. 

Thus we can work around before publish with dirty empty commits 

```bash
git commit --allow-empty -m "Empty-Commit" && git push
```
That makes sense versioning control, team work.

```bash
act -g | l ...
act --help
```
Ship with [input](https://github.com/nektos/act#flags) and [var && env](https://github.com/nektos/act/issues/279)

```rust
println!("aaaa");
```