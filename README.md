# DeepCode Git Training

Repository bài tập **Git Branch & Workflow** — bài tổng hợp cuối khóa.

📄 **[Xem toàn bộ bài làm: BAI-LAM.md](./BAI-LAM.md)**

## Repo liên quan
| Repo | Nội dung |
|---|---|
| [git-training](https://github.com/ducthuyencb/git-training) | Bài 1–12 |
| [ecommerce](https://github.com/ducthuyencb/ecommerce) | Bài 13 |
| [team-project](https://github.com/ducthuyencb/team-project) | Bài 14 |
| deepcode-git-training | Bài tổng hợp (repo này) |

## Cấu trúc branch
```
main
│
└── develop
     ├── feature/auth
     ├── feature/course
     ├── feature/payment
     ├── feature/logging
     ├── feature/report
     └── bugfix/login
```
Luồng phát hành: `feature/* → develop → test → main → production`

version: 1.2.0
