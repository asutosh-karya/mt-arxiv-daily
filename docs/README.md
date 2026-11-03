<p align="center">
  <h1 align="center"><br><ins>MT-ARXIV-DAILY</ins><br>Automatically Update MT Papers Daily using Github Actions</h1>
 
</p>



##

This repository hosts the source code for mt-arxiv-daily, scripts that fetch machine translation papers from arXiv.

## Overview

This codebase is composed of the following parts:

- `daily_arxiv.py`: main script that processes the given configuration
- `config.yaml`: configuration file of papers' keywords and so on

## Usage

<details>
  <summary>Table of Contents</summary>

1. Fork this [repo](https://github.com/asutosh-karya/mt-arxiv-daily)
2. Edit configs:
    - Change `GITHUB_USER_NAME` and `GITHUB_USER_EMAIL` in [mt-arxiv-daily.yml](../.github/workflows/mt-arxiv-daily.yml) and [update_paper_links.yml](../.github/workflows/update_paper_links.yml)
    - Change `user_name` and `repo_name` in [config.yaml](../config.yaml)
    - Push changes to the remote repo
3. Config Github Actions
    - Enable read and write permissions: Settings -> Actions -> Workflow permissions, select `Read and write permissions` and save.
    - Enable workflows: Actions -> `I understand my workflows, go ahead and enable them` -> Select `Run Arxiv Papers Daily` in the right sidebar and click `Enable workflow` -> click `Run workflow` and wait until the update job finishes. Do the same for `Run Update Paper Links Weekly`.
4. Setting GitHub Pages (optional)
    - Settings -> Pages -> Build and deployment. Source: `Deploy from a branch`; Branch select `main` and the `/docs` folder, then save.
    - The site is then available at `https://<github_username>.github.io/mt-arxiv-daily`.
5. Add new keywords (optional)
    - Edit `keywords` in [config.yaml](../config.yaml). You can add more filters or keywords.
    - Push changes to the remote repo and re-run GitHub Actions manually.
6. Archive (optional)
    - `README.md` / `docs/index.md` only keep the latest `max_papers_in_readme` papers of each keyword, since GitHub stops rendering markdown files beyond 512 KB.
    - All papers are archived by year, one markdown per keyword: `docs/archive/<year>/<Keyword>.md`, shared by the README and the gitpage, see `archive_dir` in [config.yaml](../config.yaml).
7. Code links
    - PapersWithCode is gone, so code links are looked up from the paper's abstract, [Hugging Face papers](https://huggingface.co/papers) and GitHub code search (README files citing the arXiv id).
    - The GitHub search needs `GITHUB_TOKEN` (set by the workflows) and allows 10 requests per minute, so it only runs in the weekly `Run Update Paper Links Weekly` job, which re-checks at most `max_code_checks` papers without code published within `code_check_days`, least recently checked first (`docs/code-checks.json` remembers the checks). Run `python daily_arxiv.py --update_paper_links --code_check_days 0 --max_code_checks 2000` locally to backfill older papers.

</details>

## Release plan

 We are still in the process of fully releasing. Here is the release plan:

- [x] Configuration file
- [x] Update code link
- [ ] Subscribe & Update alerting
- [ ] Support more `arxiv` filters
- [x] Archive old papers
- [ ] Language translation ([`ChatGPT`](https://chat.openai.com/chat))
- [ ] Useful comments
- [ ] ...
