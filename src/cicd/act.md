## ACT

[https://github.com/nektos/act](https://github.com/nektos/act)

GitHub Actions does not support local execution like `gitlab-runner exec ...` [here](https://gitlab.com/gitlab-org/gitlab-runner).

So this tool is a playground for local development.

Thus we can work around the issue before publishing with dirty empty commits 

```bash
git commit --allow-empty -m "Empty-Commit" && git push
```
This makes sense for version control and teamwork.

```bash
act -g | l ...
act --help
```
Ship with [input](https://github.com/nektos/act#flags) and [var && env](https://github.com/nektos/act/issues/279)

```rust
println!("aaaa");
```