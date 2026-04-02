Stop any running Jekyll containers, then start a fresh one with live reload.

```bash
cd /c/Users/XPS83/Documents/GitHub/PepperXu.github.io && docker compose down 2>&1; docker compose run --service-ports --rm jekyll-site sh -lc "bundle install; bundle exec jekyll serve -H 0.0.0.0 -w --config _config.yml,_config_docker.yml --livereload --force_polling"
```

Run the above bash command. The site will be available at http://localhost:4000. Note that _config.yml changes require a full restart to take effect.
