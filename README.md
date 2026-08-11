![License](https://img.shields.io/github/license/Infosecdecompress/Security_Interview_Questions?label=License) ![Last commit](https://img.shields.io/github/last-commit/Infosecdecompress/Security_Interview_Questions?label=Last%20Update)

# 資安面試問題 Security Interview Questions

這裡整理了一些在面試和準備美國資安相關職位時可能會問到的問題與解答，希望能幫助其他想踏入資安圈的人在找工作上更順利。目前內容都是以英文／美國資安工作為主，歡迎大家幫忙翻譯或是補充台灣求職時可能會遇到的問題。

I collected and organized some of the questions that might be asked during interviews for security-related positions, along with answers. Most of the content is in English and based on my experience in the US — translations into Mandarin and other languages, or additional content, are very welcome.

## 🌐 Website

**[jobs.infosecdecompress.com](https://jobs.infosecdecompress.com)**

The site is built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and deployed to GitHub Pages automatically on every push to `master` (see [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)).

## 📚 Contents

All content lives in [`docs/`](docs/). Each topic is one page:

| Topic | Source |
| :--- | :--- |
| Application Security | [docs/application-security.md](docs/application-security.md) |
| Encryption & Authentication | [docs/encryption-authentication.md](docs/encryption-authentication.md) |
| Network & Network Security | [docs/network-security.md](docs/network-security.md) |
| Cryptography | [docs/cryptography.md](docs/cryptography.md) |
| Security & Risk Management | [docs/risk-management.md](docs/risk-management.md) |
| Security Ops & Incident Response | [docs/secops-incident-response.md](docs/secops-incident-response.md) |
| Penetration Testing | [docs/penetration-testing.md](docs/penetration-testing.md) |
| Threat Modeling | [docs/threat-modeling.md](docs/threat-modeling.md) |
| System Admin | [docs/system-admin.md](docs/system-admin.md) |
| Security-Related Coding | [docs/security-coding.md](docs/security-coding.md) |
| Behavioral Questions | [docs/behavioral.md](docs/behavioral.md) |
| Interview & Study Tips | [docs/interview-tips.md](docs/interview-tips.md) |

## 🤝 Contributing 一起貢獻

* **Add a question or answer** — open a Pull Request editing the matching page in `docs/`. 有想分享的面試問題或補充答案，歡迎直接建 Pull Request。
* **Spot a mistake** — open an Issue if a classification, question, or answer is wrong. 分類、題目或答案有錯，歡迎建 Issue。
* **Suggest better structure** — start a Discussion. 如果覺得分類有誤或能更好地分類，歡迎在 Discussions 討論。

## 🛠️ Running the site locally

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>. Edit any file under `docs/` and the preview reloads automatically. Run `mkdocs build --strict` to reproduce the CI build.

## 📄 License & credits

Great thanks to [Grace Nolan](https://github.com/gracenolan) for sharing her [Interview Study Notes](https://github.com/gracenolan/Notes) and allowing their integration into this project.

Content is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
